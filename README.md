# Framewise Polyphonic Transcription 2016
- this repository contains code to reproduce results from a paper about framewise polyphonic piano transcription (https://arxiv.org/abs/1612.05153)

- the code is ported from theano+lasagne to pytorch 0.4.1

- obtain the MAPS dataset (http://www.tsi.telecom-paristech.fr/aao/en/2010/07/08/maps-database-a-piano-database-for-multipitch-estimation-and-automatic-transcription-of-music/)

- clone this repository

- you'll need python >= 3.5, and a CUDA installation if you want to use a GPU

- you don't need to install anything from within this repo, but you'll need to install some required python packages
```
$ pip install -r requirements.txt
```

- you'll then need to generate the (non-overlapping) splits (called `Configuration II` in the paper), by pointing the helper script to the folder that has the MAPS data:
```
$ python create-non-overlapping-splits.py <MAPS-install-directory>/data
```

- this will create a directory `non-overlapping`, containing three textfiles `train`, `valid` and `test`, which contain (audiofile, midifile) pairs

- the following call will start training the VGG-style network, and keep track of progress in `<result-directory>
```
$ python train.py non-overlapping <result-directory>
```

- you can track progress visually by using tensorboard
```
$ tensorboard --logdir <result-directory>
```

- you can evaluate a network-state by using
```
$ python evaluate.py <result-directory>/best_valid_loss_net_state.pkl <split-directory>
```


If you use stuff from this repository, please cite:
```
@inproceedings{kelz_etal_2016
  author    = {Rainer Kelz and
               Matthias Dorfer and
               Filip Korzeniowski and
               Sebastian B{\"{o}}ck and
               Andreas Arzt and
               Gerhard Widmer},
  title     = {On the Potential of Simple Framewise Approaches to Piano Transcription},
  booktitle = {Proceedings of the 17th International Society for Music Information
               Retrieval Conference, {ISMIR} 2016, New York City, United States,
               August 7-11, 2016},
  pages     = {475--481},
  year      = {2016}
}
```