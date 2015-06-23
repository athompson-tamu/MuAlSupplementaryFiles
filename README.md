# MuAlSupplementaryFiles

Setting up muon alignment in 73X:

The following bash commands will set up alignment in 73X. 

        cmsrel CMSSW_7_3_6_patch1
        cd CMSSW_7_3_6_patch1/src/
        cmsenv
        git clone https://github.com/cms-mual/Alignment.git -b CMSSW_7_3_X
        git clone https://github.com/cms-mual/TrackingTools.git -b CMSSW_7_3_X
        scram b -j 16
        
You may find in usefull to make these softlinks for editing commonly used files:

        ln -s Alignment/MuonAlignmentAlgorithms/scripts/createJobs.py
        ln -s Alignment/MuonAlignmentAlgorithms/python/gather_cfg.py
        ln -s Alignment/MuonAlignmentAlgorithms/python/align_cfg.py

Running a test job:

The following instructions will copy a list of needed files into your CMSSW_5_3_11/src directory and run a test job. Navigate your CMSSW_5_3_11/src directory before running. Be sure to change youremail.tamu.edu in the createJobs command if you wish.

        git clone https://github.com/cms-mual/MuAlSupplementaryFiles.git -b CMSSW_7_3_X
        cp MuAlSupplementaryFiles/* .
        cmsenv
        ./createJobs.py mc_DT-1100-110001_MC53_V15_5_3_11_abridged_ 3 muonGeometry_DT-Hw-111111_CSC-START53_v14-111111_Local.db singleMuonGun_RECO_Consolidated_1359Files_Blocks5_abridged.py --inputInBlocks -s mc_DT-1100-110001_MC53_V15_5_3_11_abridged.sh --validationLabel mc_DT-1100-110001_MC53_V15_5_3_11_abridged_ --b --user_mail youremail.tamu.edu --minTrackPt 30 --maxTrackPt 200 --maxDxy 0.2 --minNCrossedChambers 1 --residualsModel pureGaussian --peakNSigma 2. --station123params 110001 --station4params 100001 --cscparams 100001 --useResiduals 1100 --noCSC --mapplots --curvatureplots --segdiffplots --extraPlots --globalTag MC_53_V15::All --createAlignNtuple --gprcd inertGlobalPositionRcd --gprcdconnect sqlite_file:inertGlobalPositionRcd.db --noCleanUp
        . mc_DT-1100-110001_MC53_V15_5_3_11_abridged.sh

You should now see 7 jobs submitted.

Here is the command for the full run 1 command with DTs.

        ./createJobs.py mc_DT-1100-110001_MC53_V15_5_3_11_ 3 muonGeometry_DT-Hw-111111_CSC-START53_v14-111111_Local.db singleMuonGun_RECO_Consolidated_1359Files_Blocks5.py --inputInBlocks -s mc_DT-1100-110001_MC53_V15_5_3_11.sh --validationLabel mc_DT-1100-110001_MC53_V15_5_3_11_ --b --user_mail youremail.tamu.edu --minTrackPt 30 --maxTrackPt 200 --maxDxy 0.2 --minNCrossedChambers 1 --residualsModel pureGaussian --peakNSigma 2. --station123params 110001 --station4params 100001 --cscparams 100001 --useResiduals 1100 --noCSC --mapplots --curvatureplots --segdiffplots --extraPlots --globalTag MC_53_V15::All --createAlignNtuple --gprcd inertGlobalPositionRcd --gprcdconnect sqlite_file:inertGlobalPositionRcd.db --noCleanUp