
  436  cd dev_files && ls
  437  ls -la
  438  chmod 777 dev_file.txt
  439  sudo chmod 777 dev_file.txt
  440  ls -la
  441  su aditya-dev
  442  sudo su aditya-dev
  443  sudo vim /etc/sudoers
  444  sudo apt-get install acl
  445  whoami
  446  getfacl dev_files
  447  getfacl /home/aditya-dev/dev-files
  448  sudo getfacl dev_file.txt
  449  sudo getfcl /home/aditya-dev/dev_files
  450  sudo getfacl /home/aditya-dev/dev_files.txt
  451  sudo getfacl /home/aditya-dev/dev_file/dev_file.txt
  452  ls
  453  sudo getfacl /home/aditya-dev/dev_files/dev_fiel.txt
  454  sudo getfacl /home/aditya-dev/dev_files/dev_file.txt
  455  cd /
  456  whoami
  457  # Let's give aditya user rwe permission of file dev_file.txt
  458  sudo setfacl -m u:aditya:rwe /home/aditya-dev/dev_files/dev_file.txt
  459  # Let's give aditya user rwe permission of file dev_file.txt
  460  sudo setfacl -m u:aditya:rwx /home/aditya-dev/dev_files/dev_file.txt
  461  sudo getfacl /home/aditya-dev/dev_files/dev_file.txt
  462  whoami
  463  cat /home/aditya-dev/dev_files/dev_file.txt
  464  touch /home/aditya-dev/dev_files/dev_files.txt
  465  echo "user Aditya is wrting in the file dev_file.txt : Namaste file " > /home/aditya-dev/dev_files/dev_file.txt
  466  cat /home/aditya-dev/dev_files/dev_file.txt
  467  sudo reboot
  468  ddlsllal;j;lasdjf
  469  cd /
  470  whoami
  471  cat /home/aditya-dev/dev_files/dev_file.txt
  472  sudo vim /home/aditya-dev/dev_files/dev_file.txt
  473  cat /home/aditya-dev/dev_files/dev_file.txt
  474  # Let's serach for the keywork devops
  475  grep devops /home
  476  grep -r devops /home
  477  grep devops /home/aditya-dev/dev_files/dev_file.txt
  478  grep -r devops /home/aditya-dev/dev_files
  479  grep -r -i devops /home/aditya-dev/dev_files
  480  grep -ri t* /home
  481  grep -ri
  482  grep -ri /
  483  history
  484  grep -ri t* /home/aditya-dev
  485  grep -ir t* /home/aditya-dev
  486  sudo grep aditya-dev /etc/passwd
  487  history
  488  histroy
  489  histry
  490  history
  491  cd /'
  492  cd /
  493  ls
  494  touch log_file.txt
  495  vim log_file.txt
  496  cat vim log_file.txt
  497  grep -i error log_file.txt
  498  awk '/ERROR/ {print NR $1 $2 $4 $5}' log_file.txt
  499  awk '/ERROR/ {print NR $1, $2, $4, $5}' log_file.txt
  500  awk '/ERROR/ {print NR,$1,$2,$4}' log_file.txt
  501  awk '{NR>1 && NR<52} /ERROR/ {print}' log_file.txt
  502  awk '{NR>1 && NR<52} /INFO/ {print NR}' log_file.txt
  503  awk '{NR>1 && NR>10} /ERROR/ {print NR}' log_file.txt
  504  awk 'NR>1 && NR>10 && /ERROR/ {print NR}' log_file.txt
  505  awk 'NR>1 && NR<10 && /ERROR/ {print NR}' log_file.txt
  506  awk '{NR>1 && NR<10} && /ERROR/ {print NR}' log_file.txt
  507  awk 'NR>1 && NR<20 && /ERROR/ {print NR,$1,$3,$4} log_file.txt
  508  ":
  509  awk 'NR>1 && NR<20 && /ERROR/ {print NR,$1,$3,$4}' log_file.txt
  510  awk 'NR>1 && NR<50 && /ERROR/ {print NR,$1,$2,$4,$5,$6}' log_file.txt
  511  awk '{NR>1 && NR<10} && /ERROR/ {print NR}' log_file.txt
  512  awk 'NR>1 && NR<50 && /ERROR/ {print NR,$1,$2,$4,$5,$6}' log_file.txt && touch Error_upto_50.txt && > Error_upto_50.txt
  513  ls
  514  cat Error_upto_50.txt
  515  rm Error_upto_50.txt
  516  ls
  517  touch Error_upto_50.txt && awk 'NR>0 && NR<51 && /ERROR/ {print NR,$1,$2,$4,$5,$6}' > Error_upto_50.txt
  518  touch Error_upto_50.txt && awk 'NR>0 && NR<51 && /ERROR/ {print NR,$1,$2,$4,$5,$6}' log_file.txt > Error_upto_50.txt
  519  ls
  520  cat Error_upto_50.txt
  521  ssh
  522  history
  523  cd /
  524  sudo useradd test-user
  525  sudo cat /etc/passwd/
  526  sudo cat /etc/passwd
  527  clear
  528  sudo passwd test-user
  529  sudo cat /etc/passwd
  530  clear
  531  sudo useradd test-user -m
  532  sudo cat /etc/passwd
  533  sudo vim /etc/passwd
  534  sudo cat /etc/passwd
  535  sudo vim /etc/passwd
  536  sudo cat /etc/passwdc
  537  sudo cat /etc/passwd
  538  sudo useradd test-user -m
  539  sudo cat /etc/group
  540  sudo vim /etc/group
  541  sudo cat /etc/group
  542  sudo useradd user-test -m
  543  sudo passwd user-test
  544  sudo cat /etc/passwd
  545  sudo cat /etc/group
  546  clear
  547  sudo su user-test
  548  sudo groupadd qa-team
  549  sudo cat /etc/group
  550  clear
  551  sudo gpasswd aditya,user-test
  552  whoami
  553  sudo gpasswd -m aditya,user-test
  554  sudo gpasswd -M aditya,user-test
  555  ls
  556  sudo cat /etc/group
  557  sudo gpasswd -M aditya,user-test
  558  sudo gpasswd aditya,user-test
  559  sudo gpasswd -M aditya,user-test
  560  sudo gpasswd -M aditya,user-test qa-team
  561  sudo cat /etc/group
  562  sudo vim sudoers
  563  sudo vim /etc/sudoers
  564  sudo ls -la /etc/group
  565  sudo ls -l /etc/group
  566  sudo ls -ra /etc/group
  567  sudo cat /etc/group
  568  ls -la
  569  sudo cd /etc/group
  570  sudo ls -la /etc/group
  571  cd /etc/group
  572  cd /etc/
  573  ls
  574  cd group
  575  cd f group
  576  cat group
  577  ls -la
  578  ls -la group
  579  ../
  580  cd /
  581  sudo /etc/sudoers
  582  cd /etc/sudoers
  583  sudo cd /
  584  cd /etc/passwd
  585  sudo cat /etc/group
  586  sudo cat ls -la /etc/group
  587  pwd
  588  sudo cat /etc/sudoers
  589  sudo vim /etc/sudoers
  590  su user-test
  591  sudo reboot
  592  sudo ls -la /etc/passwd
  593  sudo cat /etc/passwd
  594  ls -la
  595  clear
  596  cd/
  597  cd /
  598  whoami
  599  cd /home/user-test
  600  sudo cd/home/user-test
  601  sudo cd /home/user-test
  602  cd /home/user-test
  603  cd /h ome
  604  cd /home
  605  ls
  606  cd /aditya-devops
  607  cd ./aditya-devops/
  608  cd ../
  609  cd ./user-test
  610  cd ./user-test/
  611  ls -la
  612  sudo reboot
  613  clear
  614  su user-test
  615  clear
  616  cd /
  617  ls -la /etc/passwd
  618  sudo cat /etc/sudoers | grep qa-team
  619  clear
  620  whoami
  621  cd /home/
  622  cd /aditya
  623  cd ./aditya
  624  cd ../
  625  cd ./user-test
  626  su user-test
  627  cd aditya
  628  ls
  629  cd /home/aditya/.viminfo:> /mnt/h/MORK/adityaubantu/log_file.txt
  630  cd ../
  631  cd H:
  632  cd :H
  633  cd /mnt/h/MORK/adityaubantu
  634  ls
  635  grep ERROR ./log_file.txt
  636  grep ERROR ./Error_upto_50.txt
  637  grep "ERROR" ./log_file.txt
  638  grep ERROR /log_file.txt
  639  grep -r -i ERROR ./log_file.txt
  640  grep -r -i ERROR ./Error_upto_50.txt
  641  cd ./log_file.txt
  642  cd f ./log_file.txt
  643  cat ./log_file.txt
  644  cat ./Error_upto_50.txt
  645  sudo vim ./log_file.txt
  646  cat ./log_file.txt
  647  cp ./log_file.txt ./logcopy_file.txt
  648  ls
  649  cat ./logcopy_file.txt
  650  cat ./log_file.txt
  651  grep -i ERROR ./log_file.txt
  652  cd /
  653  grep -r -i devops /home
  654  sudo find /home -perm 777
  655  sudo find/home -perm 560
  656  sudo find /home -perm 560
  657  find /home -type f -perm 777
  658  sudo find /home -type f -perm 777
  659  sudo find /home  f -perm 777
  660  grep log_file.txt /
  661  grep log_file.txt /home
  662  grep -r log_file /home
  663  cd /mnt/h/MORK/adityaubantu
  664  ls
  665  awk '/ERROR/ {print NR}' log_file.txt
  666  awk '/ERROR/ {print NR, $1, $2, $3}' log_file.txt
  667  awk 'NR>=5 && NR<=15 {print NR,$0}' logfile.txt
  668  awk 'NR>=5 && NR<=15 {print NR,$0}' /log_file.txt
  669  awk 'NR>=5 && NR<=15 {print NR,$0}' log_file.txt
  670  cd /
  671  cd ~
  672  pwd
  673  touch team.txt
  674  ls -la
  675  chmod 600 team.txt
  676  ls -la
  677  chomd 644 team.txt
  678  chmod 644 team.txt
  679  ls -la
  680  touch secure.sh
  681  ls
  682  chmod 601 secure.sh
  683  ls -la
  684  touch notes.txt
  685  ls -la
  686  chmod 000 notes.txt
  687  ls -la
  688  cat notes.txt
  689  rm {notes.txt,secure.sh,team.txt}
  690  ls
  691  sudo notes.txt
  692  sudo rm notes.txt
  693  ls
  694  cd ../
  695  ls
  696  cd ~
  697  pwd
  698  touch acl_test.txt
  699  ls
  700  setfacl u:test-user:r acl_test.txt
  701  --help
  702  setfacl --help
  703  setfacl -M u:user-test:r acl_test.txt
  704  setfacl -m u:user-test:r /acl_test.txt
  705  ls
  706  setfacl -m u:user-test: ./acl_test.txt
  707  getfacl ./acl_test.txt
  708  setfacl -m u:user-test:r ./acl_test.txt
  709  getfacl ./acl_test.txt
  710  setfacl -m u:user-test:rw ./acl_test.txt
  711  getfacl ./acl_test.txt
  712  setfacl -x u:user-test: ./acl_test.txt
  713  getfacl ./acl_test.txt
  714  chmod 600 ./acl_test.txt
  715  getfacl ./acl_test.txt
  716  setfacl -m g:qa-team:rw ./acl_test.txt
  717  getfacl ./acl_test.txt
  718  whoami
  719  su user-test
  720  pwd
  721  ls
  722  getfacl ./acl_test.txt
  723  sudo awk '/qa-team/ {print}' /etc/group
  724  su user-test
  725  grep -r -i sudo /etc/
  726  top
  727  sudo apt-get update
  728  sudo apt-get install docker
  729  docker --version
  730  sudo apt-get install docker.io
  731  top
  732  tob -b
  733  top -b
  734  top -b | head -3
  735  top -b | -5
  736  top -b | head -5
  737  top -b | head -10
  738  systemctl status docker
  739  systemctl status sshd
  740  whoami
  741  pwd
  742  ls
  743  mkdir
  744  mkdir my_scripts
  745  ls
  746  cd my_scripts
  747  ls
  748  vim firstScript.sh
  749  cat vim firstScript.sh
  750  ls -la
  751  ls
  752  chmod 700 firstScript.sh
  753  ls
  754  ls -la
  755  chmod 700 firstScript.sh
  756  ls -la
  757  sudo chmod 700 firstScript.sh
  758  ls -la
  759  mount | grep /mnt/h
  760  rm -r my_scripts
  761  rm -r /
  762  cd ../
  763  rm -r my_scripts
  764  ls
  765  cd /
  766  cd /home/aditya
  767  pwd
  768  ls
  769  mkdir my_scripts
  770  cd my_scripts && vim firstScript.sh
  771  ls
  772  ls -la
  773  chmod 700 firstScript.sh
  774  ls
  775  bash firstScript.sh
  776  ./firstScript.sh
  777  cd ../
  778  ls
  779  l
  780  cd my_scripts
  781  l
  782  vim make_folder_file.sh
  783  l
  784  chmod 700 make_folder_file.sh
  785  ls -la
  786  bash make_folder_file.sh
  787  cd /home/aditya
  788  ls
  789  cd my_scripts
  790  l
  791  vim make_folder_file.sh
  792  l
  793  rm new_file.txt
  794  l
  795  rm -rf new_folder
  796  l
  797  bash make_folder_file.sh
  798  l
  799  cd new_folder
  800  ls
  801  cd ../
  802  cat new_file.txt
  803  rm new_file.txt && rm -rf new_folder
  804  l
  805  vim make_folder_file.sh
  806  bash make_folder_file.sh
  807  vim make_folder_file.sh
  808  bash make_Folder_file.sh
  809  bash make_folder_file.sh
  810  l
  811  cd new_folder
  812  ls
  813  cd ../
  814  rm new_file.txt
  815  ls
  816  l
  817  vim make_folder_file.sh
  818  cat /new_folder/new_file.txt
  819  cd new_folder
  820  ls
  821  cat new_file.txt
  822  date
  823  data | awk '{print $1,$2}'
  824  date | awk '{print $1,$2}'
  825  awk /date/ '{print $1,$2}'
  826  cd /
  827  cd ~
  828  ls
  829  cd /mnt/h/MORK/adityaubantu
  830  ls
  831  awk /ERROR/ '{print NR,$1,$2}' ./log_file.txt
  832  awk /ERROR/ '{print NR,$1,$2}' log_file.txt
  833  awk '/ERROR/ {print NR,$1,$2}' log_file.txt
  834  cd /
  835  cd ~
  836  ls
  837  cd my_scripts
  838  ls
  839  date
  840  vim date_day_month.sh
  841  ubantu --version
  842  --version
  843  exit
  844  wsl --unregister <DistroName>
  845  wsl ubantu --version
  846  wsl --list --verbose
  847  wsl -l -v
  848  wsl -d Ubuntu --version
  849  exit
  850  cd H
  851  cd ../
  852  ls
  853  cd ubuntu-aws-key
  854  ls
  855  ls -la
  856  chmod 400 ubantu-aws.pem
  857  ls
  858  ls -la
  859  ssh -i "ubantu-aws.pem" ubuntu@ec2-51-21-2-232.eu-north-1.compute.amazonaws.com
  860  cdmod 400 ubantu-aws.pem
  861  chmod 400 ubantu-aws.pem
  862  ls -la
  863  exit
  864  history
  865  cd /
  866  cd ~
  867  ls
  868  cd my_scripts
  869  l
  870  date
  871  vim date_day_month.sh
  872  l
  873  ls -la
  874  chmod 700 date_day_month.sh
  875  l
  876  ls -la
  877  ./date_day_month.sh
  878  rm date_day_month.sh
  879  ls
  880  date
  881  timedatectl
  882  date
  883  vim date_month_time.sh
  884  chmod 700 date_month_time.sh
  885  l
  886  ./date_month_time.sh
  887  cp date_month_time.sh day_month_date.sh
  888  l
  889  rm day_month_date.sh
  890  l
  891  mv date_month_time.sh day_month_date.sh
  892  ./day_month_date.sh
  893  vim day_month_date.sh
  894  echo $SHELL
  895  who
  896  who -H
  897  ls
  898  vim firstScript.sh
  899  ./firstScript.sh
  900  vim firstScript.sh
  901  ./firstScript.sh
  902  uptime -H
  903  uptime
  904  who -H
  905  -F
  906  -f
  907  ls
  908  -f day_month_date.sh
  909  vim checkFileExists.sh
  910  chmod 700 checkFileExists.sh
  911  l
  912  ./checkFileExists.sh
  913  vim checkFileExists.sh
  914  ./checkFileExists.sh
  915  vim checkFileExists.sh
  916  vim chekFileExistsWithArgs.sh
  917  chmod 700 checkFileExistsWithArgs.sh
  918  ls
  919  mv chekFileExistsWithArgs.sh checkFileExistsWithArgs.sh
  920  ls
  921  chmod 700 checkFileExistsWithArgs.sh
  922  ./checkFileExistsWithArgs.sh
  923  ./checkFileExistsWithArgs.sh firstScript.sh make_folder.sh somethingelse
  924  vim checkFileExistsWithArgs.sh
  925  ./checkFileExistsWithArgs.sh firstScript.sh make_folder.sh somethingelse
  926  vim checkFileExistsWithArgs.sh
  927  vim ForLoop.sh
  928  chmod 700 ForLoop.sh
  929  l
  930  ./ForLoop.sh
  931  vim ForLoop.sh
  932  ./ForLoop.sh
  933  vim ForLoop.sh
  934  ./ForLoop.sh
  935  vim ForLoop.sh
  936  ./ForLoop.sh
  937  ./ForLoop.sh 20
  938  vim ForLoop.sh
  939  ./ForLoop.sh
  940  ./ForLoop.sh 20
  941  vim ForLoop.sh
  942  ./ForLoop.sh
  943  ./ForLoop.sh 20
  944  vim ForLoop.sh
  945  ./ForLoop.sh 20
  946  vim ForLoop.sh
  947  ./ForLoop.sh 20
  948  vim ForLoop.sh
  949  ./ForLoop.sh 20
  950  vim ForLoop.sh
  951  ./ForLoop.sh 20
  952  ./ForLoop.sh 200
  953  vim ForLoop.sh
  954  df -H
  955  df -H | xargs
  956  free -h
  957  free -h | xargs
  958  echo "the available RAM is : " && free -h | xargs | awk '{print $10, "/
  959  ", $8}'
  960  echo "the available RAM is : " && free -h | xargs | awk '{print $10,"/",$8}'
  961  whoam i
  962  whoami
  963  cd /
  964  ls
  965  ssh user@server_ip
  966  ssh
  967  ls
  968  cd H:
  969  cd H/
  970  cd ../
  971  cd :/mnt/h/MORK/
  972  cd /mnt/h/MORK
  973  ls
  974  cd adityaubantu
  975  ls
  976  cd ../
  977  cd ubantu-aws-key
  978  cd ubuntu-aws-key
  979  ls
  980  cd /
  981  cd ~
  982  whoami
  983  pwd
  984  mkdir ubantu-aws-key
  985  l
  986  cd /mnt/h/MORK/ubuntu-aws-key
  987  cp ubantu-aws.pem /home/aditya/ubantu-aws-key
  988  cd /home/aditya/ubantu-aws-key
  989  ls
  990  clear
  991  ls
  992  chmod 400 ubantu-aws.pem
  993  ls -la
  994  ec2-51-20-63-119.eu-north-1.compute.amazonaws.com
  995  ubuntu@ec2-51-20-63-119.eu-north-1.compute.amazonaws.com
  996  ssh ubuntu@ec2-51-20-63-119.eu-north-1.compute.amazonaws.com
  997  ssh -i ubantu-aws.pem ubuntu@ec2-51-20-63-119.eu-north-1.compute.amazonaws.com
  998  exit
  999  cd /
 1000  cd ~
 1001  pwd
 1002  ls
 1003  mkdir gen_keys && touch gen_PrKey.pem
 1004  ls
 1005  cd gen_keys
 1006  ls
 1007  l
 1008  touch gen_PrKey.pem
 1009  ls
 1010  vim gen_PrKey.pem
 1011  cat gen_PrKey.pem
 1012  cd ~
 1013  ls
 1014  cd gen_keys
 1015  ls
 1016  ssh -i gen_PrKey.pem ec2-51-20-92-15.eu-north-1.compute.amazonaws.com
 1017  ssh -i gen_PrKey.pem ubantu@ec2-51-20-92-15.eu-north-1.compute.amazonaws.com
 1018  ssh -i gen_PrKey.pem ubauntu@ec2-51-20-92-15.eu-north-1.compute.amazonaws.com
 1019  ssh -i gen_PrKey.pem ubuntu@ec2-51-20-92-15.eu-north-1.compute.amazonaws.com
 1020  chmod 400 gen_PrKey.pem
 1021  ssh -i gen_PrKey.pem ubuntu@ec2-51-20-92-15.eu-north-1.compute.amazonaws.com
 1022  cd /
 1023  cd ~
 1024  ls
 1025  whoami
 1026  cd practice1
 1027  ls
 1028  vim from_local.txt
 1029  cat from_local.txt
 1030  scp -i /home/aditya/ubantu-aws-key/ubantu-aws.pem from_local.txt ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:/home/ubantu
 1031  scp -i /home/aditya/ubantu-aws-key/ubantu-aws/pem from_local.txt ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:/home/ubuntu
 1032  whoami
 1033  clear
 1034  cd /home/aditya/ubantu-aws-key
 1035  cd /practice1
 1036  cd ../
 1037  ls
 1038  cd practice1
 1039  clear
 1040  whoami
 1041  ls
 1042  scp -i cd /home/aditya/ubantu-aws-key/ubantu-aws.pem from_local.txt ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:/home/ubuntu
 1043  scp -i cd /home/aditya/ubantu-aws-key/ubantu-aws.pem from_local.txt ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:/home/ubuntu/
 1044  clear
 1045  ls
 1046  cat from_local.txt
 1047  scp -i /home/aditya/ubantu-aws-key/ubantu-aws.pem from_local.txt ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:/home/ubuntu
 1048  # successfuly file copied to server
 1049  clear
 1050  # now copying a file from the server to client
 1051  whoami
 1052  scp -i /home/aditya/ubantu-aws-key/ubantu-aws.pem ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:from_server.txt /
 1053  scp -i /home/aditya/ubantu-aws-key/ubantu-aws.pem ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com:/home/ubuntu/from_server.txt .
 1054  ls
 1055  cat from_server.txt
 1056  # remember (.) this dot represent current folder
 1057  cd .
 1058  exit
 1059  cd ~
 1060  ls
 1061  cd gen_keys
 1062  ls
 1063  ssh gen_PrKey.pem -i ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com
 1064  ssh -i gen_PrKey.pem ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com
 1065  clear
 1066  cd /
 1067  cd ~
 1068  ls
 1069  rm gen_PrKey.pem
 1070  ls
 1071  ls ubantu-aws-key
 1072  cd ubantu-aws-key
 1073  ssh -i ubantu-aws.pem ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com
 1074  s
 1075  ls
 1076  ssh -i ubantu-aws.pem ubuntu@ec2-51-21-129-16.eu-north-1.compute.amazonaws.com
 1077  cd /home/aditya
 1078  ls
 1079  cd ubantu-aws-key
 1080  ls
 1081  cd /
 1082  cd /home/aditya/ubantu-aws-key
 1083  cd /
 1084  cat /home/aditya/ubantu-aws-key/ubantu-aws.pem
 1085  clear
 1086  cd /
 1087  cd ~
 1088  pwd
 1089  whoami
 1090  clear
 1091  pws
 1092  pwd
 1093  clear
 1094  pwd
 1095  ls
 1096  cd my_scripts
 1097  ls
 1098  touch assignment1.sh
 1099  ls
 1100  chmod 700 assigment1.sh
 1101  chmod 700 assignment1.sh
 1102  ls -la
 1103  echo "Hello $(whoami)"
 1104  date
 1105  echo "Data : $(date | awk '{print $1,"/",$2,"/",$3}'"
 1106  date
 1107  echo "DATE : $(date | awk '{print $1,"/",$2,"/",$3}')"
 1108  echo "Time : $(date | awk '{print $4}'
 1109  "
 1110  echo "Time : $(date | awk '{print $4}'"
 1111  echo "Time : $(date | awk '{print $4}')"
 1112  nmcli con show
 1113  hostname
 1114  history
 1115  uptime -h
 1116  uptime
 1117  uptime
 1118  uptime -H
 1119  uptime
 1120  clear
 1121  sudo uptime -H
 1122  uptime
 1123  who
 1124  who -H
 1125  su aditya-devops
 1126  -F
 1127  -h
 1128  user
 1129  fuser
 1130  fuser -a
 1131  clear
 1132  uptime
 1133  who
 1134  clear
 1135  bondlamamoduttecasy
 1136  clear
 1137  uptime
 1138  uptime -H
 1139  uptime -p
 1140  uptime -s
 1141  uptime -V
 1142  time
 1143  uptime
 1144  who
 1145  daemon
 1146  systemd
 1147  system
 1148  history