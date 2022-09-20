# score-based-channels
Source code for estimating MIMO channels using score-based (diffusion) models. See citations for paper references.

Generic flow:
1. Use ```matlab/main.m``` to generate training, validation and test channels.
2. Use ```train.py``` to train a deep score-based model for channel estimation with the default parameters used in the paper.
3. Use ```hyperparam_tuning.py``` to find ```beta``` and ```N```, exactly like in the paper.

3.1. The script will contain a saved variable ```oracle_log```, which contains the NMSE with respect to the ground truth channels, for all the hyper-parameters, noise levels, and each invididual sample.

3.2. Averaging the error across all samples ```(axis=-1)``` and using ```argmax``` over the corresponding axes will return the best hyper-parameters for each invididual SNR point (in a loop, assuming known SNR, or also averaged across SNR in the blind setting).

4. Use ```inference.py``` to perform inference with the hyper-parameters found before.
5. (Optional, incomplete) Use ```train_wgan.py``` to train a WGAN model.
6. Use ```matlab/test_end_to_end.m``` with ```target_channels = 'ours_known'``` to simulate the end-to-end setup used in the paper: 4 streams of QPSK over 16 x 64 CDL-C channels. Make sure that ```target_file``` was generated by ```inference.py```.

# TODO
- Create Google Colab demo w/ pretrained models.
- Pre-generate data to remove dependency on Matlab NR Toolbox.
- Completely remove dependency on Matlab.

# Citations
Full credits for the ncsnv2 repository go to: https://github.com/ermongroup/ncsnv2

Please include the following citations when using or referencing this codebase:

```
@article{arvinte2022mimo,
  title={MIMO Channel Estimation using Score-Based Generative Models},
  author={Arvinte, Marius and Tamir, Jonathan I},
  journal={arXiv preprint arXiv:2204.07122},
  year={2022}
}

@inproceedings{arvinte2022score1,
  title={Score-Based Generative Models for Wireless Channel Modeling and Estimation},
  author={Arvinte, Marius and Tamir, Jonathan},
  booktitle={ICLR Workshop on Deep Generative Models for Highly Structured Data},
  year={2022}
}

@inproceedings{arvinte2022score2,
  title={Score-Based Generative Models for Robust Channel Estimation},
  author={Arvinte, Marius and Tamir, Jonathan I},
  booktitle={2022 IEEE Wireless Communications and Networking Conference (WCNC)},
  pages={453--458},
  year={2022},
  organization={IEEE}
}
```
