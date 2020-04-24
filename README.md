# SoalShiftSISOP20_modul4_T21
Soal Shift Sistem Operasi 2020


Hisyam Zulkarnain F             05311840000019\
Bayu Trianayasa                 05311840000038
## #4 &ndash; Log System
---


```
#define FUSE_USE_VERSION 28
#include <fuse.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
#include <dirent.h>
#include <errno.h>
#include <sys/time.h>

static const char *dirpath = "/home/osboxes/modul4";
static const char *infodir = "/home/osboxes/fs.log";

void write_log(int numlevel,char *command,char *one,char *two){
    FILE *f = fopen(infodir,"a+");
    
    char loginfo[1000],level[50];
    int year,month,day,hour,minute,second;

    time_t curtime;
    struct tm* loc_time;
    time(&curtime);
    loc_time = localtime(&curtime);
    year  = (loc_time->tm_year + 1900)%1000;
    month = loc_time->tm_mon+1;
    day   = loc_time->tm_mday;
    hour  = loc_time->tm_hour;
    minute= loc_time->tm_min;
    second= loc_time->tm_sec;
    
    memset(level,0,50*sizeof(char));
    if(numlevel==0){    
        strcpy(level,"WARNING");
    } else {
        strcpy(level,"INFO");
    }

    memset(loginfo,0,1000*sizeof(char));
    if(two==NULL){
        sprintf(loginfo,"%s::%d%d%d-%d:%d:%d::%s::%s",level,year,month,day,hour,minute,second,command,one);
    } else {
        sprintf(loginfo,"%s::%d%d%d-%d:%d:%d::%s::%s::%s",level,year,month,day,hour,minute,second,command,one,two);
    }
    
    fprintf(f,"%s\n",loginfo);
    fclose(f);
}
 ```
