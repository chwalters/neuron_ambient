# intelora-Ambient_sound

A Neuron that provides background sound for focusing or creating a relaxing ambiance

## Synopsis

Make Intelora play background ambient sounds for establishing a relaxing ambiance.

## Installation

Install the neuron into your resource directory
```bash
intelora install --git-url https://github.com/intelora/neuron_ambient.git
```

## Options

| parameter         | required | type   | default          | choices             | comment                                                                     |
|-------------------|----------|--------|------------------|---------------------|-----------------------------------------------------------------------------|
| state             | YES      | string |                  | "on", "off"         | Target state of the ambient sound.                                          |
| sound_name        | NO       | string |                  | See the list bellow | If not set, a sound will be selectedrandomly                                |
| mplayer_path      | NO       | string | /usr/bin/mplayer |                     | Path to mplayer binary. By default /usr/bin/mplayer on Debian family system |
| auto_stop_minutes | NO       | int    |                  | Integer > 1         | Number of minutes before Intelora stop automatically the background sound   |

List of available sound:
- birds
- fireplace
- forest
- forest-rain
- forest-stream
- heavy-rain
- mountain-steam
- ocean-waves
- seaside
- stream
- summer-rain
- thunderstorm
- tropical-beach
- tropical-thunderstorm
- urban-thunderstorm
- wind
- wood-sailboat


## Return Values

| Name             | Description                             | Type   | sample                                                   |
|------------------|-----------------------------------------|--------|----------------------------------------------------------|
| playing_sound    | The current sound played                | string | fireplace                                                |
| available_sounds | List of available sound in the database | list   | ['fireplace', 'heavy-rain', 'tropical-beach', 'seaside'] |

## Limitation
-Only available sounds in the database:
birds
fireplace
forest
forest-rain
forest-stream
heavy-rain
mountain-steam
ocean-waves
seaside
stream
summer-rain
thunderstorm
tropical-beach
tropical-thunderstorm
urban-thunderstorm
wind
wood-sailboat
-Auto stop after 20 minutes
-The user will add their own sound file inside the "sound" folder.

## Synapses example

Start an ambient sound randomly
```yml
- name: "ambient-random"
  signals:
    - order: "ambient sound"
  neurons:
    - ambient_sound:
        state: "on"
```

```yml
- name: "ambient-stop"
  signals:
    - order: "stop ambient sound"
  neurons:
    - ambient_sound:
        state: "off"
```

Play selected ambient sound
```yml
- name: "ambient-random"
  signals:
    - order: "ambient sound"
  neurons:
    - ambient_sound:
        state: "on"
        sound_name: "forest-rain"
```

Auto stop after 20 minutes
```yml
- name: "ambient-sleep"
  signals:
    - order: "ambient sound before sleeping"
  neurons:
    - ambient_sound:
        state: "on"
        auto_stop_minutes: 20
        say_template:
            - "I've selected {{ playing_sound }}"
```

## Notes

You add your own sound file inside the "sound" folder.

## Licence

MIT
