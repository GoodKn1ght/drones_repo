# drones_repo




https://www.youtube.com/watch?v=NV2hqw8wu3U



https://www.youtube.com/playlist?list=PLQQ577DOyRN_hY6OAoxBh8K5mKsgyJi-r


```pip install "isaacsim[all,extscache]==5.1.0" --extra-index-url https://pypi.nvidia.com```



https://developer.nvidia.com/isaac/sim



https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/pip_installation.html

https://docs.isaacsim.omniverse.nvidia.com/4.5.0/core_api_tutorials/tutorial_core_hello_world.html

https://lycheeai-hub.com/isaac-lab/build-your-own-isaac-lab-external-project-template-generator

https://lycheeai-hub.com/isaac-lab/gallery-of-content/installation-guide


```# # # # import time
# # # # from isaac_sim import IsaacApp
# # # # from omni.isaac.core import World
# # # # from omni.isaac.core.prims import XformPrim
# # # # from omni.isaac.core.articulations import Articulation

# # # # # Ініціалізація додатку
# # # # app = IsaacApp()

# # # # # Створення світу (сцени)
# # # # world = World()

# # # # # Створення куба
# # # # cube = XformPrim(prim_path="/World/Cube")
# # # # cube.create_prim()
# # # # cube.set_translation([0, 0, 0.5])  # Встановлюємо куб у висоту

# # # # # Додавання артикуляції
# # # # articulation = Articulation(prim_path="/World/ArticulatedObject")
# # # # articulation.create_prim()

# # # # # Запуск симуляції
# # # # while True:
# # # #     world.step()
# # # #     time.sleep(0.016)  # 60 FPS




# # # from isaacsim import SimulationApp

# # # # Ініціалізація SimulationApp перед імпортами інших модулів
# # # simulation_app = SimulationApp({"headless": False})

# # # # Тепер можна імпортувати інші модулі
# # # from isaacsim import SimulationApp
# # # from isaacsim.core.api import World
# # # from isaacsim.core.prims import SingleXFormPrim
# # # import time

# # # # Створення світу
# # # world = World()

# # # # Створення куба
# # # cube = SingleXFormPrim(prim_path="/World/Cube")  # Використовується SingleXFormPrim
# # # cube.create_prim()
# # # cube.set_translation([0, 0, 0.5]) 

# # # # # Додавання артикуляції
# # # # articulation = Articulation(prim_path="/World/ArticulatedObject")
# # # # articulation.create_prim()

# # # # Запуск симуляції
# # # while True:
# # #     world.step()  # Оновлюємо світ
# # #     time.sleep(0.016)  # Затримка для симуляції, щоб вона працювала з 60 FPS



# # from isaacsim import SimulationApp
# # simulation_app = SimulationApp({"headless": False})

# # # Спробуйте імпортувати Stage замість World
# # from isaaclab.sim import sim_utils
# # from isaacsim.core.prims import DynamicCuboid
# # import numpy as np
# # import asyncio

# # async def main():
# #     # Створення сцени
# #     stage = Stage()
# #     await stage.initialize_simulation_context_async()

# #     # Додаємо підлогу
# #     stage.scene.add_default_ground_plane()

# #     # Створення динамічного куба
# #     cube = stage.scene.add(
# #         DynamicCuboid(
# #             prim_path="/World/cube",  # шлях до примітива
# #             name="my_cube",
# #             position=np.array([0.0, 0.0, 1.0]),  # початкова позиція
# #             scale=np.array([0.5, 0.5, 0.5]),
# #             color=np.array([0.0, 0.0, 1.0])  # колір
# #         )
# #     )

# #     # Скидаємо та запускаємо симуляцію
# #     await stage.reset_async()
# #     await stage.start_async()

# #     # Виконуємо декілька кроків симуляції
# #     for _ in range(500):
# #         await stage.step_async()

# #     # Зупиняємо симуляцію
# #     await stage.stop_async()

# # # Запуск асинхронної функції
# # if __name__ == "__main__":
# #     loop = asyncio.get_event_loop()
# #     loop.run_until_complete(main())



#launch Isaac Sim before any other imports
#default first two lines in any standalone application
from isaacsim import SimulationApp
simulation_app = SimulationApp({"headless": False}) # we can also run as headless.

from isaacsim.core.api import World
from isaacsim.core.api.objects import DynamicCuboid
import numpy as np

world = World()
world.scene.add_default_ground_plane()
fancy_cube =  world.scene.add(
    DynamicCuboid(
        prim_path="/World/random_cube",
        name="fancy_cube",
        position=np.array([0, 0, 1.0]),
        scale=np.array([0.5015, 0.5015, 0.5015]),
        color=np.array([0, 0, 1.0]),
    ))
# Resetting the world needs to be called before querying anything related to an articulation specifically.
# Its recommended to always do a reset after adding your assets, for physics handles to be propagated properly
world.reset()
for i in range(500):
    position, orientation = fancy_cube.get_world_pose()
    linear_velocity = fancy_cube.get_linear_velocity()
    # will be shown on terminal
    print("Cube position is : " + str(position))
    print("Cube's orientation is : " + str(orientation))
    print("Cube's linear velocity is : " + str(linear_velocity))
    # we have control over stepping physics and rendering in this workflow
    # things run in sync
    world.step(render=True) # execute one physics step and one rendering step

simulation_app.close() # close Isaac Sim
```


```
from pegasus.simulator.params import SIMULATION_ENVIRONMENTS
from pegasus.simulator.logic.interface.pegasus_interface import PegasusInterface

# Start the Pegasus Interface
pg = PegasusInterface()

# Set the default PX4 installation path used by the simulator
# This will be saved for future runs
pg.set_px4_path("path_to_px4_directory")
```
