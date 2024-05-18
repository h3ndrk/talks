# vRoHOW Demo Plot

## Preparation

- Reconnect VPN (ensure it will not disconnect)
- Close additional browser and terminal windows
- Hidden Connect to Rechenknecht with tmux
- Make sure the neural networks are running
- Open Terminal window
- First tab
  - Split into 4 cell grid
  - Enable "Synchronize input"
  - `ssh rechenknecht.hulks.dev`
  - `cd rohow-2020/nao-bitvector-string/tools/machine-learning`
  - Disable "Synchronize input" on the lower right
  - In the upper left: `source venv/bin/activate`, `clear`
  - In the lower right: `cd generic/distributed_task_execution_framework/producer/frontend`, `clear`
  - Disable "Synchronize input" on all cells
- Second tab
  - Split into 10 cell grid
  - Enable "Synchronize input"
  - `ssh rechenknecht.hulks.dev`
  - `cd rohow-2020/nao-bitvector-string/tools/machine-learning`
  - `source venv/bin/activate`
  - `clear`
- Rename tabs: "Bitvector", "Additional Bitvector Workers"
- Increase font size in each terminal cell
- In Rechenknecht tmux: Open `~/rohow-2020/nao-bitvector-string/tools/machine-learning/generic/distributed_task_execution_framework/worker/genetic_individual_bitvector/ditef_worker_genetic_individual_bitvector`
  - `cp __init__.py.fast __init__.py`

After preparation:

- Hidden screen
  - this Demo Plot
  - Rechenknecht tmux
    - Bitvector worker directory open
  - Reveal.JS speaker notes
- Shared screen
  - Terminal
    - 4x fast bitvector
    - 10x slow bitvector
  - Browser
    - [Bitvector frontend](http://134.28.57.202:3001)
    - [Neuralnet frontend](http://134.28.57.202:3000)
    - Reveal.JS presentation

## Live

Setting: on the slide "Live-Demo"

Say: We have now seen our theoretical approach but now we want to show you that it works in practice.

Next slide: "Live-Demo: Bitvector" (bullet points)

Say: The first individual we implemented was the bitvector individual. It solves the so called one-max-problem, which is a common example from the literature. It is also often used as an introductioral optimization problem for genetic algorithms.

Say: As mentioned before, a individual is defined by a genome and the fitness. The genome is sequence of bits, fitness sums up number of true bits, genetic algorithm optimizes for maximizing fitness.

Next slide: "Live-Demo: Bitvector" (single worker diagram)

Say: Here, we see the setup of the bitvector evaluation that we will show you in a minute.

Say: On the left: task producer, consisting of a backend and frontend. The backend runs the genetic algorithm which generates tasks for the distributed task execution framework. The frontend serves our user interface via a web browser.

Say: In the middle: task router, central component of the whole demo setup

Say: On the right: one bitvector worker, it gets the bitvector genome, the sequence of bits, calculates the sum/fitness and returns it back to the backend

Say: Next, we will setup the three left processes, but without the worker. After that, I will quickly show you our user interface and we then start a bitvector worker (the node that you can see on the right).

Switch to terminal

Say: First, I will start the task router, the central component containing the task queues which coordinates the tasks from the producers to the workers.

`ditef-router --port 8082`

Say: The next step is to start the backend.

`ditef-producer-genetic-algorithm-sliding --port 8083 --population-tasks 11 http://localhost:8082/ ditef_producer_genetic_individual_bitvector`

Say: This command enables the bitvector individual in the genetic algorithm which means that this task producer now produces tasks for the bitvector workers (which we will start in a minute).

Say: The last process, for now, is the frontend which serves the user interface.

`BROWSER=none PORT=3001 yarn start`

Say: This takes a few seconds to start. Once started we can head over to the web browser and navigate to the started frontend. ... As a short recap while we wait for the frontend: The user interface, we will see shortly, allows us to add or remove genetic populations or change the configuration at runtime. In addition, we are able to inspect a running genetic algorithm with all its parameters.

Wait for the frontend

Switch to web browser, reload http://134.28.57.202:3001

Say: Here, you can see the current list of populations. We didn't add any so this list is currently empty. In the lower right corner, I can add a new population.

Click on +-Button

Say: As mentioned before, each population has its own configuration. For example, we can change the intended population size, probabalistic weights and individual settings. In the bottom, there is the `genome_size` which controls how large the bitvector is, which we want to optimize now. Let's add the population with these settings.

Click Add-Button

Say: Our new population is now shown in the list with some current metrics. Remember: We didn't start a worker yet and that's the reason why this population does not change currently. Let's investigate this population.

Click on population

Say: Within one population, we can observe some important metrics in more detail. At the top, there are two charts about the size and fitness over time. They are emtpy, because of the not started worker. At the bottom, we can see the list of members contained in this population. They are currently waiting to be evaluated but there is no worker at the moment. Therefore they have not got a fitness. Let's look at one individual.

Click on individual

Say: The individual page shows detailed informations about one individual. At the top, we can see the genome. Here you can see the bitvector in action. Each red portion corresponds to a false bit, all the green ones to a true bit. The goal of this algorithm is to evolve the individuals over time so that this genome visualization gets more green, the maximum reachable fitness is 100, because our bitvector has this amount of bits. Currently this individual has no fitness and since it is a random generated individual, it does not have any parents. Let's go back to the population page.

Go back in browser

Say: I think, we are now ready to see the genetic algorithm in action. For that I will finally start the worker.

Switch to terminal

`ditef-worker http://localhost:8082/ ditef_worker_genetic_individual_bitvector`

Switch to browser

Say: As you can see, the population slowly progresses and increases its fitness.

Wait for some time

Say: Let's look at one individual.

Open one best individual

Say: Now, you can see here, that this individual has nearly converged with the optimal solution. It has a fitness of .... At the bottom, you can now see that this individual got generated by a cross over/clone operation and that it served as parent for several children.

Go to population list, remove population

Switch to presentation

Say: I want to show you now, that we are able to attach not only one worker to the algorithm, but many.

Next slide: "Live-Demo: Bitvector" (multiple worker diagram)

Say: We will first start a population with one worker and I will then connect more workers to the router. Hopefully, we can see a steep increase in the fitness plot. Let's see.

Switch to terminal, kill worker

In Rechenknecht tmux, run `cp __init__.py.slow __init__.py`

Restart worker `ditef-worker http://localhost:8082/ ditef_worker_genetic_individual_bitvector`

Switch to browser, create a population with maximum size 35

Say: We see on the top right a slow increase of the fitness. Let's start more workers.

Switch to terminal, to 10-cell tab

Start 10 workers `ditef-worker http://localhost:8082/ ditef_worker_genetic_individual_bitvector`

Switch to browser

Say: As you can see, the average fitness increases much more quickly. Starting more workers has an immediate effect on the speed of our genetic algorithm implementation.

Go to population list, remove population

Switch to presentation

Next slide: "Live-Demo: Neural Networks" (bullet points)

Say: We have another demo prepared for you. Now we are looking at our main topic of this talk: Evolving neural networks with our genetic algorithm. With this demo we want to show you, that our implementation is capable of coming up with good-performing and efficient neural networks. Because of our individual abstraction, we can simply swap out the bitvector individual with a neural network one. Again, the question is, how is the genome and fitness defined. As mentioned before, we are representing the neural network architecture and hyperparameters as genome. The fitness is then simply the accuracy on some test dataset. Similar to the bitvector example, we want to maximize the fitness. ... As training neural networks may take a long time, we started the genetic algorithm for this demonstration a few days ago. We have connected 12 heterogeneous workers to it. The setup is very similar to the bitvector example.

Next slide: "Live-Demo: Neural Networks" (multiple worker diagram)

Say: The setup contains the four component types: a backend with an attached frontend, the router in the middle, and several task workers. Let's see that in action.

Switch to browser tab, http://134.28.57.202:3000, start in population list

Say: The neural network setup currently consists of a single population.

Open population

Say: We can see that the best members are around 0.88 (eighty-eight).

Scroll a little bit through the member list, show unevaluated individuals

Say: Now let's look at one of the best individuals.

Open best individual

Say: At the top you can see the genome again. For this individual type we tried to profit from the web-based user interface which allows to display rich visualizations of the individuals. We are training a positioner neural network which gets an image as input and outputs the position of a potential ball on this image. The fitness of this neural network is .... For the neural network individual we added a computational cost penalty to the fitness which allows us to make the algorithm prefer more efficient individuals. On the right, we are displaying the training progression over the training epochs. And below all that fancy stuff, we also have the genealogy of this individual again. The genealogy allows us for example to identify genetic operations that produce bad individuals or, in contrast, work well.

Switch to presentation

Next slide: "/Live-Demo"

Say: So much for the live demonstration. We have now shown you that our approach works in practice. ... What do we conclude from it?

Next slide: "Conclusions"

Say: The distributed task execution framework allows to scale the task execution horizontally and vertically by attaching additional task workers to the task router.

Next bullet point "Population and individual level concurrency"

Say: Within the algorithm, or task producer, the iteration loop may be executed multiple times in parallel to increase concurrency of the individual evaluation.

Next bullet point "Selective execution for heterogeneous resources"

Say: The task workers request tasks from the router by only requesting their supported types. This allows the workers to select which task types they want to execute. This feature can be used to distribute work selectively across the workers by configuring which types they should request from the router. The system is robust against network failures, by simply resuming once the connection is re-established. We have seen this during the live demonstration where I dynamically attached and detached workers.

Next two bullet points "Algorithm abstraction" & "Suggestion abstraction"

Say: The abstractions introduced by our implementation within one task producer allows to swap algorithms and individuals without overhead. This is achieved by introducing a common interface between algorithms and individuals. Individuals provide methods for executing genetic operations which are called by the algorithm.

Next bullet point "Evaluation code separation"

Say: Code seperation in our framework allows us to run tasks with vastly different dependencies without requiring all nodes of our network to fulfill these requirements.

Next bullet point "Inference library compatibility"

Say: The neural network individual evaluation concludes with checking whether the trained neural network performs as expected in the inference library used on the robots.

Say: With that let's look at things we might look at in the future.

Next slide: "Outlook"

Say: We are planning to apply our genetic algorithm to other problem domains, such as robot motion, game state estimation, and robot role assignments. We might also implement different solution suggestion algorithms instead of a genetic algorithm, such as tree search or particle swarm optimizers. As we've seen in the demonstration, task workers can be executed in any environment evaluating vastly different tasks. We therefore might also try to run task workers directly on the NAO robot, to evaluate for example walking parameters directly on the hardware.

Next slide: "Thank you for listening"

Say: With that, we would like to thank you for listening. What questions do you have?
