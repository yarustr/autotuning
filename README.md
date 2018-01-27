# ethos-auto-tuning
Ethos ccminer auto gpu core memory and power tuning 

To get it to your rig run command on terminal:
git clone https://github.com/yarustr/autotuning


EASY CONFIG AND USAGE

Be sure that you are connected to the internet.

Disable remote.conf. To disable remote.conf delete or comment everything inside that file. Backup your local.conf. When the test finish you must restore your local.conf

The next step is to make autotuning file executable. Just type the following command to the terminal and press enter:

chmod +x /home/ethos/autotuning/autotuning

Add the command below before line "exit 0" in the file /home/ethos/custom.sh 
 
((sleep 60;echo "/n"; lxterminal  --command /home/ethos/autotuning/autotuning) &)


If you do not have any experience with tuning of rigs, please use the default settings. !STRONGLY ADVISED TO USE DEFAULTS

Settings are located at /home/ethos/autotuning/config.txt
Test results are located at /home/ethos/autotuning/pass.txt

When the testing is finished, you can set your rig for max hash or for low power, or max hash/power....
You can even draw graphs from results /home/ethos/autotuning/pass.txt for visual analysis.


After the test/tunning is finished:
Delete or comment the command added to /home/ethos/custom.sh which is "((sleep 60;echo "/n"; lxterminal  --command /home/ethos/autotunning/autotunning) &)"
Restore /home/ethos/local.conf from your backup.

Copy cor,mem and pwr settings to your /home/ethos/local.conf then run the following command from the terminal:

minestop && disallow && sleep 5 && putconf && ethos-overclock && sleep 5 && minestop && allow



Supported algorithm are :
bitcore
blake2s
blakecoin
c11
cryptonight
equihash
Groestl
keccak
lyra2v2
myr-gr
neoscrypt
nist5
quark
qubit
scrypt
skein
skunk
tribus
x11
x17
xevan


If this is useful to you PLEASE consider a donation for my hard work:
BTC : 36Ei4suDRMKHuHqGKJ5LMEgACzE6b85SFY
ETH : 0xaf0af98b90580e855c6b6815d9ba67b5fc4bef8f
Dash: XdvLdX1iXocG4vcb6jjT4dQHKT8pvLcEJZ
LTC : Lb1hcjjfKaxg7DeLqAbDe1QDD16MsX1B4M
XRP : destination tag 299737064		add: rhL5Va5tDbUUuozS9isvEuv7Uk1uuJaY1T


Below you can find the settings. All start with # 

1. setting is #miner. Auto tuning supports only ccminer at the moment. Keep it as it is.
Example: 
#miner ccminer

2. setting is #algo. Here you must define which algorithm you want to use.							
Example:
#algo nist5

3. setting is #flags. Here you can set flags of the ccminer. If you do not know or are not sure, please use the default settings.
Example:
#flags   -i 26 --submit-stale

4. setting is #maxgputemp. Set maximum temperature allowed for GPUs. It is a global setting.
Example:
#maxgputemp   85

5. setting is #globalfan. Set fan spin percentage. It is a global setting.
Example:
#globalfan  85

6. setting is #cenable. To enable core tuning for GPUs set to 1. To disable core tuning for GPUs set to 0.
Example:
#cenable 1

7. setting is #menable. To enable memory frequency tuning set to 1. To disable memory frequency tuning set to 0.
Example:
#menable 1

8. setting is #penable. To enable power tuning set 1. To disable power tuning set to 0.
Example:
#penable 1

9. setting is #cor. This is a step counter and must be set to 0 for a new test. It will increase until #cor equals to #cmaxsteps value
Example:
#cor 0

10. setting is #mem. This is a step counter and must be set to 0 for a new test. It will increase until #mem equals to #mmaxsteps value
Example:
#mem 0

11. setting is #pwr. This is a step counter and must be set to 0 for a new test. It will increase until #pwr equals to #pmaxsteps value
Example:
#pwr 0

12. setting is #cstep. Here you can set a step decrease for #maxplus. For example - if the maximum value is +180(#maxplus 180) and #cstep is 5, 180 will decrease by 5. 180, 175, 160, 165....  
Example:
#cstep 5

13. setting is #mstep. Here you can set a step decrease for memory frequency. For example - if the maximum supported memory freq. for gpu  is 5000 mgh and #mstep is 250, 5000 will decrease by 250. 5000, 4750, 4500, 4250....  
Maxs supported value is set before and you do not need to set it.
Example:
#mstep 250

14. setting is #pstep. Here you can set a step decrease for GPU's maximum power. For example - if the maximum supported power for gpu is 250 and #pstep 5, 250 will decrease by 5. 250, 245, 240, 235....  
Maxs supported value is set before and you do not need to set it.
Example:
#pstep 5

15. setting is #cmaxsteps. The test of all GPU core frequencies will continue until #cor equals to #cmaxsteps. ONLY IF 6. SETTING is set to 1 (enabled).
Example:
#cmaxsteps 25

16. setting is #mmaxsteps. The memory frequency test will continue until #mem equals to #mmaxsteps. ONLY IF 7. SETTING is set to 1 (enabled).
Example:
#mmaxsteps 10

17. setting is #pmaxsteps. The power test will continue until #pwr equals to #pmaxsteps. ONLY IF 8. SETTING is set to 1 (enabled).
Example:
#pmaxsteps 30

18. setting is #useclockplusstyle. It will enable the "+" setting style for GPUs core freq. testing. For NVDIA GPUs is better to use "+" style. To enable the "+" style set to 1, to disable - set to 0.
Example:
#useclockplusstyle 1

19. setting is #maxplus. If the "+" style core testing is set by  #useclockplusstyle to 1 , then #maxplus will be used. 
Example:
#maxplus 180

20. setting is #initwaitseconds. This setting is used to set a waiting time for the miner after the testing starts. If any of the GPUs failed, the rig will be restarted. 120 seconds is the optimum waiting time. Do not set it too low (minimum 60 second recomended), otherwise a false GPU fail will be detected.
Example:
#initwaitseconds 120

21. setting is #checkeveryseconds. Sets the check time after initial waiting time passes. If any of the GPUs has failed, the rig will be restarted.
Example:
#checkeveryseconds 60

22. setting is #testminutes. Sets the minutes for the test. To consider the test settings STABLE, minimum 20 minutes test is adviced.
Example:
#testminutes 20

------------------------------------------------------------------------------------------------------------------------------
When you are ready with the settings, restart your rig and the test will start automatically. You can follow it from the terminal, which will open on startup.
To terminate the testing process, press ctrl+c. If you do not delete or comment the command in /home/ethos/custom.sh, which is:

"((sleep 60;echo "/n"; lxterminal  --command /home/ethos/autotunning/autotunning) &)"

the test will continue when the rig restarts.

And again - if it is useful to you PLEASE consider a donation for my hard work:
BTC : 36Ei4suDRMKHuHqGKJ5LMEgACzE6b85SFY
ETH : 0xaf0af98b90580e855c6b6815d9ba67b5fc4bef8f
Dash: XdvLdX1iXocG4vcb6jjT4dQHKT8pvLcEJZ
LTC : Lb1hcjjfKaxg7DeLqAbDe1QDD16MsX1B4M
XRP : destination tag 299737064		add: rhL5Va5tDbUUuozS9isvEuv7Uk1uuJaY1T



