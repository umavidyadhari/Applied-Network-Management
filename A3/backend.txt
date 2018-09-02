#!/usr/bin/python
import sys
import subprocess
import shlex
import os
from subprocess import Popen,PIPE,STDOUT
sys.argv[0] = "/tmp/A2/prober";
#sys.argv[1] = "prober";
sys.argv.insert(0,"unbuffer");
sys.argv.insert(4,"-1");
print sys.argv;
l=len(sys.argv);
a=l-5;


"""
for i in sys.argv:
 print sys.argv[5:];
"""
p = subprocess.Popen(sys.argv, stdout=subprocess.PIPE)
line = p.stdout.readline()
#print line,
while line:
 l=line.split('|')
 #print sys.argv[5:];
 #print l[0]
 for i in range(a):
  print i;
  print 'rate,oid=%s value=%.0f time=%d' % (sys.argv[i+5],float(l[1]),int(l[0]));
  os.system("curl -i -XPOST 'http://localhost:8086/write?db=A3&u=ats&p=atslabb00&precision=s' --data-binary 'rate,oid='%s' value=%.0f %d'"% (sys.argv[i+5],float(l[i+1]),int(l[0]) ) );


 #curl -i -XPOST 'http://localhost:8086/write?db=A3&u=ats&p=atslabb00' --data-binary 'rate,oid= value= time,'


    ##oid,rate,time

 line = p.stdout.readline()


