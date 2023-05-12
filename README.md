# 3D-sandbox-game
A big flat world where you can build, destroy and parkour in full screen and a FPS counter in top-right. If you want to close the game press ALT+f4
here is code incase also press enter after you copy paste if game is not working and ALT+F4 to close game
from ursina import *
from ursina.prefabs.first_person_controller import FirstPersonController

app = Ursina()

window.fullscreen = True  # Set to fullscreen
window.fullscreen_size = (1920, 1080)  # Set resolution of fullscreen display
window.position = (0, 0)  # Move window to top-left corner of screen

class Voxel(Button):
    def __init__(self, position=(0, 0, 0)):
        super().__init__(
            parent=scene,
            position=position,
            model='cube',
            origin_y=.5,
            texture='white_cube',
            color=color.color(0, 0, random.uniform(.9, 1.0)),
            highlight_color=color.lime,
        )

for z in range(60):
    for x in range(60):
        voxel = Voxel(position=(x, 0, z))


def input(key):
    if key == 'left mouse down':
        hit_info = raycast(camera.world_position, camera.forward, distance=5)
        if hit_info.hit:
            Voxel(position=hit_info.entity.position + hit_info.normal)
    if key == 'right mouse down' and mouse.hovered_entity:
        destroy(mouse.hovered_entity)


player = FirstPersonController()
app.run()
