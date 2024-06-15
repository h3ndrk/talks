title.pdf: title.svg many_robots_on_field.jpg zuehlke.png profile.jpg
	svg2pdf title.svg title.pdf

robocup.pdf: robocup.svg rescue.jpg at_home.jpg at_work.jpg logistics.jpg small_size.jpg mid_size.jpg humanoid.jpg simulation.jpg spl.jpg many_robots_on_field.jpg
	svg2pdf robocup.svg robocup.pdf

spl_and_nao.pdf: spl_and_nao.svg nao_kicks_ball.jpg
	svg2pdf spl_and_nao.svg spl_and_nao.pdf

team.pdf: team.svg team.jpg gore.jpg rohow.jpg rohow2.jpg
	svg2pdf team.svg team.pdf

stepspline2.png: stepspline2.svg
	resvg --dpi 200 stepspline2.svg stepspline2.png

robot_control_software.pdf: robot_control_software.svg nao_walking_in.jpg camera_top.jpg camera_bottom.jpg stepspline2.png
	svg2pdf robot_control_software.svg robot_control_software.pdf

software_design.pdf: software_design.svg two_naos_fighting_for_ball.jpg
	svg2pdf software_design.svg software_design.pdf

transition_0.pdf: transition_0.svg nao_looking_into_field.jpg
	svg2pdf transition_0.svg transition_0.pdf

transition_1.pdf: transition_0.svg transition_1.svg nao_looking_into_field.jpg
	svg2pdf transition_1.svg transition_1.pdf

transition_2.pdf: transition_1.svg transition_2.svg nao_looking_into_field.jpg
	svg2pdf transition_2.svg transition_2.pdf

current_state.pdf: current_state.svg nao_kicks_ball2.jpg
	svg2pdf current_state.svg current_state.pdf

demo.pdf: demo.svg nao_feet.jpg
	svg2pdf demo.svg demo.pdf

outro.pdf: outro.svg empty_field_from_above.jpg link_github.svg link_talks.svg zuehlke.png profile.jpg
	svg2pdf outro.svg outro.pdf

slides.pdf: title.pdf robocup.pdf spl_and_nao.pdf team.pdf robot_control_software.pdf software_design.pdf transition_0.pdf transition_1.pdf transition_2.pdf current_state.pdf demo.pdf outro.pdf
	pdfunite title.pdf robocup.pdf spl_and_nao.pdf team.pdf robot_control_software.pdf software_design.pdf transition_0.pdf transition_1.pdf transition_2.pdf current_state.pdf demo.pdf outro.pdf slides.pdf
