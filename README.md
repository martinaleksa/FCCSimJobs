# FCCGunLHE
[]() Clone and initialisation
-------------------------

If you do not attempt to contribute to the repository, simply clone it:
```
git clone git@github.com:clementhelsens/FCCSimJobs.git
```

If you aim at contributing to the repository, you need to fork and then clone the forked repository:
```
git clone git@github.com:YOURGITUSERNAME/FCCSimJobs.git
```

[]() Sending simulation jobs
-------------------------
Various options are available and are explained below. 
1. First if **--singlePart** is used, the following options are possible:
   - **--particle** for the particle ID. The supported ones are 11(e-), -11(e+), -13(mu-), 13(mu+), 22, 111(pi0), 211(pi+), -211(pi-), 130(K0L). For example to run single anti-muon, use **--particle -13**
   - the angle is changed using **--phiMin** and **--phiMax**, default are 0 and 2pi respectively
   
   
2. Second if **--physics** is used, the following options are possible
   - **--process** to select the type of process. Two types are available
      - from LHE events, this will call a gun that will produce 2 back to back objects, the following keys are available **ljets**, **top**, **Wqq**, **Zqq**, **Hbb**. If this option is used, the pt can also be given using **--pt**
      - from calling pythia8 direcly, thus generating the events at 100TeV, the following keys are available **MinBias**, **Haa**, **Zee**, **H4e**
      
      
3. Third there are common options
   - the pseudo-rapidity range is changed using **--etaMin** and **--etaMax**, default is 0 for both 
   - the batch system is either **--lsf**  or **--condor**
   - the number of events per job is configured through **-n**
   - and the number of jobs to send is configured through **-N**
   
4. Running examples are:

```
python send.py --singlePart --particle 11 -e 500 -n 10 -N 1 --condor --etaMin 3.5 --etaMax 3.5
python send.py --singlePart --particle -211 -e 10 -n 10 -N 1 --condor
python send.py --physics --process Zqq --pt 1000 -n 10 -N 1 --lsf
python send.py --physics --process Haa -n 10 -N 1 --lsf
```

5. Also, please often check the afs directory where the jobs where send, because there will be the log files stored there as well as the output root file when running on condor (needs to be understood)

6. Few times a day, a script will run to check the jobs that have been processed and the results will be published on this webpage
http://fcc-physics-events.web.cern.ch/fcc-physics-events/FCCsim_v01.php

7. Once in a while you can run the clean script to remove all the jobs that are marked as failed in the database.
This is something that can not be done centrally yet as I do not have rights to remove files I haven't produced.


