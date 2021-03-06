## Available variables
Definitions: 
```C++
ElectronIDHelper * eIDHelper_;
float radius = 3.; // cylinder radius around shower axis
eIDHelper_->computeHGCAL(electron,radius);

LongDeps ld(eIDHelper_->energyPerLayer(radius,true));

float measuredDepth, expectedDepth, expectedSigma;
float depthCompatibility = eIDHelper_->clusterDepthCompatibility(ld,measuredDepth,expectedDepth, expectedSigma);
```

In case of gsfElectrons, all shower variables are calculated for the `electron.electronCluster()` object.

| Variable | For ID | Description | Access method |
| ------------- | ------------- | ----- | ----- |
| | | **Cluster shapes** |
| `sigmaUU` | :white_check_mark: | Perpendicular cluster spread| `eIDHelper_->sigmaUU()` |
| `sigmaVV` | :white_check_mark: | Radial cluster spread | `eIDHelper_->sigmaVV()` |
| `sigmaEE` | :x: | Cluster spread in eta | `eIDHelper_->sigmaEE()` |
| `sigmaPP` | :x: | Cluster spread in phi | `eIDHelper_->sigmaPP()` |
| | | **Longitudinal / energy** | |
| `nLayers` | :white_check_mark: | Numer of layers in cluster | `ld.nLayers()` |
| `firstLayer` | :white_check_mark: | First layer of cluster | `ld.firstLayer()` |
| `lastLayer` | :x: | Last layer of cluster | `ld.lastLayer()` |
| `layEfrac10` | :white_check_mark: | First layer with 10% energy in EE | To be added, present in ntuple |
| `layEfrac90` | :white_check_mark: | First layer with 90% energy in EE | To be added, present in ntuple |
| `layerEnergy` | :x: | Energy per layer | `ld.energy(layer)` |
| `energyEE` | :x: | Energy within cylinder in EE | `ld.energyEE()` |
| `energyFH` | :x: | Energy within cylinder in EE | `ld.energyFH()` |
| `energyBH` | :x: | Energy within cylinder in EE | `ld.energyBH()` |
| `FHoverE` | :white_check_mark: | Energy within cylinder in EE | `energyFH/energyEE` |
| `HoverE` | :white_check_mark: | Energy within cylinder in EE | `(energyFH+energyBH)/energyEE` |
|  | | **Depth compatibility** |   |
| `measuredDepth` | :white_check_mark: | Measured shower depth | See above |
| `expectedDepth` | :white_check_mark: | Expected shower depth | See above |
| `expectedSigma` | :white_check_mark: | Expected shower depth sigma | See above |
| `depthCompatibility` | :white_check_mark: | Depth compatibility | See above |

## Additional global variables
| `n_vtx` | :white_check_mark: | Number of reco vertices | See inputTag `offlinePrimaryVertices` |

## Additional variables for gsfElectrons
KF track requires:
```C++
reco::TrackRef myTrackRef = ele.closestCtfTrackRef();
  validKF = (myTrackRef.isAvailable());
  validKF = (myTrackRef.isNonnull());  
```

| Variable | For ID | Description | Access method |
| ------------- | ------------- | ----- | ----- |
| | | **Track-based** | Also available from gsfEle directly |
| `pOut` | :white_check_mark: | Track momentum (Pout)| `eIDHelper_->trackMomentumAtEleClus()` |
| `eOverPout` | :white_check_mark: | Electron cluster energy over Pout | `eIDHelper_->eEleClusterOverPout()` |
| | | **Cluster-track matching** |
| `deltaEta` | :white_check_mark: | dEta between Pout and cluster | `eIDHelper_->deltaEtaEleClusterTrackAtCalo()` |
| `deltaPhi` | :white_check_mark: | dPhi between Pout and cluster  | `eIDHelper_->deltaPhiEleClusterTrackAtCalo()` 
| | | **Track properties** |
| `eta` | :white_check_mark: | Track eta | `electron.eta()` |
| `fbrem` | :white_check_mark: | (Pin-Pout)/Pin | `electron.fbrem()` |
| `gsfChi2` | :white_check_mark: | Chi^2 of GSF track | `ele.gsfTrack()->normalizedChi2()` |
| `kfChi2` | :white_check_mark: | Chi^2 KF track | `myTrackRef->normalizedChi2()` |
| `kfNhits` | :white_check_mark: | Number of hits for GSF track | `myTrackRef->hitPattern().trackerLayersWithMeasurement()` |
