# MolMapNet: An Efficient Convolutional Neural Network Based on High-level Features for Molecular Deep Learning

## MolMap
MolMap is generated by the following steps:

* Step1: Data sampling 
* Step2: Feature extraction 
* Step3: Feature pairwise distance calculation --> cosine, correlation, jaccard
* Step4: Feature 2D embedding --> umap, tsne, mds
* Step5: Feature grid arrangement --> grid, scatter
* Step5: Transform --> minmax, standard
* Step6: Get MolMap


## Installation

1. install [rdkit]('http://www.rdkit.org/docs/Install.html) first:
```bash
conda create -c rdkit -n my-rdkit-env rdkit
conda activate my-rdkit-env
```
2. in your "my-rdkit-env" env, install molmap by:

```bash
git clone https://github.com/shenwanxiang/bidd-molmap.git
cd bidd-molmap
pip install -r requirements.txt --user

# add molmap to PYTHONPATH
echo export PYTHONPATH="\$PYTHONPATH:`pwd`" >> ~/.bashrc

# init bashrc
source ~/.bashrc
```

3. [deepchem]('https://github.com/deepchem/deepchem') (optional). In our paper, deepchem has been used as a dataset provider, so you may install it by:
```bash
pip install deepchem==2.2.1.dev54
```

4. If you have gcc problems when you install molmap, please installing g++ first:
```bash
sudo apt-get install g++
```


## Out-of-the-Box Usage

```python
import molmap
# Define your molmap
mp_name = './descriptor.mp'
mp = molmap.MolMap(ftype = 'descriptor', fmap_type = 'grid',
                   split_channels = True,   metric='cosine', var_thr=1e-4)
```

```python
# Fit your molmap
mp.fit(method = 'umap', verbose = 2)
mp.save(mp_name) 
```

```python
# Visulization of your molmap
mp.plot_scatter()
mp.plot_grid()
```

```python
# Batch transform 
smiles_list = ['CC(=O)OC1=CC=CC=C1C(O)=O']
X = mp.batch_transform(smiles_list,  scale = True, 
                       scale_method = 'minmax', n_jobs=4)
print(X.shape)
```



## To cite us:

* MolMapNet: An Efficient Convolutional Neural Network Based on Contructed Feature Maps for Molecular Deep Learning


