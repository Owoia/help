# help


#obj_music_1 {
Create event {
close = obj_closer_1
close_x = close.x - x;
close_y = close.y -y;

gun2 = obj_playpause_1
gun_x2 = gun2.x - x;
gun_y2 = gun2.y -y;

global.close = 0




is_dragging = false
prev_mouse_x = 0
prev_mouse_y = 0

}
}

Step event: {
if global.close = 1 {
		instance_destroy()
	}

if( is_dragging == false )
{
    if( mouse_check_button( mb_left ) )
    {
        if( collision_point( mouse_x, mouse_y, self, false, false ) )
        {
            is_dragging = true;
        }
    }
}

if( is_dragging == true )
{
    var mouse_travel_x = mouse_x - prev_mouse_x;
	var mouse_travel_y = mouse_y - prev_mouse_y;
    x += mouse_travel_x;
	y += mouse_travel_y
    prev_mouse_x = mouse_x;
	prev_mouse_y = mouse_y
}

if( !mouse_check_button( mb_left ) )
{
    is_dragging = false;
    speed = 0;
    prev_mouse_x = mouse_x;
	prev_mouse_y = mouse_y;
}

close_x = close.x - x;
close_y = close.y -y;

gun_x2 = gun2.x - x;
gun_y2 = gun2.y -y;

close.x = x + close_x
close.y = y + close_y;

gun2.x = x + gun_x2
gun2.y = y + gun_y2;
}
}
obj_playplause_1{
create event: {image_index = 1
image_speed = 0
playing = 0
}
step event: {
if global.close = 1 {
		audio_stop_sound(mus_73_7)
		instance_destroy()
	}
	
	if mouse_check_button_pressed(mb_left) && position_meeting(x, y, obj_cursorhitbox){
	if playing = 0 {
		audio_play_sound(mus_73_7, 0, 1, 0.7, 0, 1)
		playing = 1
		image_index = 0
	}
	if playing = 1 {
		audio_pause_sound(mus_73_7);
		playing = 2
		image_index = 1
	}
	if playing = 2 {
		audio_resume_sound(mus_73_7);
		playing = 1
		image_index = 0
	}
	}
}
}

and finally:
obj_closer_1:
Create: global.close = 0
step: if mouse_check_button_pressed(mb_left) && position_meeting(x, y, obj_cursorhitbox){
	global.close = 1
	alarm[0] = 1
	}
	
	if global.close = 1 {
		instance_destroy()
	}
alarm 0: global.close = 0
Sorry if that's alot!
