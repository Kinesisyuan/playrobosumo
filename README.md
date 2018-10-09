Implementing RoboSumo Environment
========
## Installation of Robosumo with its requirements

RoboSumo depends on `numpy`, `gym`, and `mujoco_py>=1.5` (if you haven't used MuJoCo before, please refer to [the installation guide](https://github.com/openai/mujoco-py)).
Running demos with pre-trained policies additionally requires `tensorflow>=1.1.0` and `click`.

The requirements can be installed via [pip](https://pypi.python.org/pypi/pip) as follows:

```bash
$ pip install -r requirements.txt
```

To install RoboSumo, clone the repository and run `pip install`:

```bash
$ git clone https://github.com/openai/robosumo
$ cd robosumo
$ pip install -e .
```

## Demos

You can run demos of the environments using `demos/play.py` script:

```bash
$ python demos/play.py
```

The script allows you to select different opponents as well as different policy architectures and versions for the agents.
For details, please refer to the help:

```bash
$ python demos/play.py --help

Usage: play.py [OPTIONS]

Options:
  --env TEXT                    Name of the environment.  [default: RoboSumo-Ant-vs-Ant-v0]
  --policy-names [mlp|lstm]...  Policy names.  [default: mlp, mlp]
  --param-versions INTEGER...   Policy parameter versions.  [default: 1, 1]
  --max_episodes INTEGER        Number of episodes.  [default: 20]
  --help                        Show this message and exit.
```

## Trying to modify the map

The system construct the environment (map) in a function in `robosumo/envs/utils.py` and related modifications to the world parameters are made when the function runs.

## Modify username of "scene catcher"
Everytime when robosumo runs, it load the model (xml) file and construct a large .xml that includes both agents and the environment. This large file called "scene.xml" are stored in a tmp directory and can be found nowhere after running, even when an error occurs. So I add some lines to `robosumo/envs/sumo.py` to catch it in order to check what problem may occur in the final xml model. Of course the path includes my username, so change it to yours before running.

## Walls Change with Size of the Map
I assume the pushable cube to be 2x2x2, and the target area to be 4x4 on one edge of the colosseum. Based on this, walls of the map can be generated according to the size that is set in `robosumo/epolicy_zoo/__init__.py`. Size = 8.0 means 8 units in each direction, thus the colosseum sizes 16x16.

## Cube still not movable
Theoretically, simply adding a free joint will make the white cube in the middle not fixed anymore, but doing so will raise a loading error which is not solved yet. Will look into it.
