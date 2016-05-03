
1. 打印第v列的和
 awk -F "\t" -v v=1 '{sum+=$v}END{print sum}' file
 
2. 打印除第v列以外的列
 awk -F "\t" -v v=3 '{
    len=split($0,arr,"\t");
    for(i=1;i<len;i++)
    if (i!=v) {a=a$i"\t"};
    if(len!=v) a=a$len;
    if(len==v) a=substr(a,1,length(a)-1);
    print a;
    a="";
 }' file
 
3. 取第v列的最小值，最大值
 awk -F "\t" -v v=1 'NR==1{max=min=$v;next}{max=max>$v?max:$v;min=min<$v?min:$v}END{print max,min}' file
 
4. 统计某一列中有多少个不同的值
 awk -v v=1 'BEGIN{FS="\t"}{a[$v]=1;sum=0} END{for(i in a) sum+=a[i];print sum}' file
 
5. 删除重复行
 awk '!a[$0]++' file 
 
6. 矩阵转置
 awk -F "\t" '{for(i=1;i<=NF;i++){a[FNR,i]=$i}}END{for(i=1;i<=NF;i++){for(j=1;j<=FNR;j++){printf a[j,i]"\t"}print ""}}' file | sed 's/[ \t]*$//' | sed '$d'
 
7. 删除文件最后一行
 sed '$d' file.txt
 
8. 删除末尾空格
 sed 's/[ \t]*$//' lr_predict_tmp > lr_predict_tmp1
 
9. 空值补0
 awk -F "\t" '{for (i=1;i<=NF;i++) if($i=="") $i=0; print $0}' OFS="\t" tt > tt2﻿​  



#/**
# * @file awk_util.sh
# * @author _iMatrix
# * @date 2015-05-22
# * @brief 使用awk的一些tips
# * @version v0.1
# **/

#!bin/sh

# 1.取出等于view的列，且合并某两列，城市id#团单id
awk '$7=="view"{print $3,$5"#"$4}' file > tmp

# 2.不排序删除重复行
awk '!a[$0]++' tmp > tmp1

# 3.将session相同的行合并
awk 'BEGIN{FS=" "} {map[$1]=map[$1]$NF" "} END{for(i in map)print i,map[i]}' tmp1 > tmp2
#awk 'BEGIN{FS=OFS=" "} {map[$1]=map[$1]$NF" "} END{for(i in map)print i,map[i]}' tmp > tmp1

# 4.取团单id列大于1的记录
awk 'NF>2{print $0}' tmp2 > tmp3

# 5.删除每一行结尾处最后的空格tab
sed 's/[ \t]*$//' tmp3 > test2

# 6.展示前件和后件
awk '{
        for(i = 3; i <= NF; i++) {
                if(i < NF) {
                    printf "%s\t%s\n",$2,$i
                }
                else {
                    print $2"\t"$i
                }
        }
}' test2 > src
awk '{for(i = 3; i <= NF; i++) {if(i < NF) {printf "%s\t%s\t%s\n",$1,$2,$i} else{print $1"\t"$2"\t"$i}}}' test2 > src2
#awk '{for(i = 3; i <= NF; i++) {if(i < NF) {printf "%s\t%s\n",$2,$i} else{print $2"\t"$i}}}' test2 > src

## 6.获得nuomi_ctr_roi_adjust_format的前件-后件
awk '{print $1"\t"$2}' nuomi_ctr_roi_adjust_format > ctr_predict

### 7.获得lr_predict的前件-后件
awk '{print $1"\t"$2}' lr_predict_ctr_join_roi_price_out > lr_predict

#### 8.src和lr_predict对比，获取交集，得到src落入lr_predict的数据
awk 'NR==FNR{a[$0]++} NR>FNR&&a[$0]' src lr_predict > lr_predict_output
# src2
# s1    A    B
# s1    A    C
# s1    A    E
# s2    B    D
# s2    B    E
# s2    B    F
# s3    A    B
# s3    A    D
# s4    E    A
# predict
# A    B
# A    C
# A    D
# B    C
# B    D
# C    E
# C    F
# C    G
awk 'NR==FNR{a[$1,$2]=1} NR>FNR&&a[$2,$3]' lr_predict src2 > lr_predict_output2

#### 8.1 验证一下，先查看一下记录
more lr_predict_output
awk '$1=="1000010000#1001987"&&$2=="1000010000#596088"{print $0}' lr_predict
awk '$1=="1000010000#1001987"&&$2=="1000010000#596088"{print $0}' src

##### 9.src和ctr_predict对比，获取交集，得到src落入ctr_predict的数据
awk 'NR==FNR{a[$0]++} NR>FNR&&a[$0]' src ctr_predict > ctr_predict_output

###### 10.统计
awk 'BEGIN{FS="\t"}{a[$1]+=1}END{for(i in a)print  i"\t"a[i]}' lr_predict_output > lr_predict_output_statistics
awk 'BEGIN{FS="\t"}{a[$1]+=1}END{for(i in a)print  i"\t"a[i]}' ctr_predict_output > ctr_predict_output_statistics

####### 11.合并结果，进行对比
awk -F "\t" 'NR==FNR{map[$1]=$2} NR>FNR{print $0"\t"map[$1]}' ctr_predict_output_statistics lr_predict_output_statistics > lr_join_ctr_statistics

######## 12.相减再合并
awk -F "\t" '{map[$1]=$2-$3;if($2-$3>0) map2[$1]=1;if($2-$3<0) map2[$1]=-1;if($2-$3==0) map2[$1]=0} {print $0"\t"map[$1]"\t"map2[$1]}' lr_join_ctr_statistics > lr_join_ctr_statistics2

######### 13.统计+1,0,-1的个数
awk 'BEGIN{FS="\t"}{a[$5]+=1}END{for(i in a)print  i"\t"a[i]}' lr_join_ctr_statistics2 > compare_result

########## 14.统计原来session中以第1个团单为前件，其后件的个数;还有lr_predict,ctr_predict后件个数
awk 'BEGIN{FS="\t"}{a[$1]+=1}END{for(i in a)print  i"\t"a[i]}' src > src_post_count
awk 'BEGIN{FS="\t"}{a[$1]+=1}END{for(i in a)print  i"\t"a[i]}' lr_predict > lr_predict_post_count
awk 'BEGIN{FS="\t"}{a[$1]+=1}END{for(i in a)print  i"\t"a[i]}' ctr_predict > ctr_predict_post_count

########### 15.将src_post_count加入到lr_join_ctr_statistics2中，方便查看
awk -F "\t" 'NR==FNR{map[$1]=$2} NR>FNR{print $0"\t"map[$1]}' src_post_count lr_join_ctr_statistics2 > lr_join_ctr_statistics2_with_src_post_count
awk -F "\t" 'NR==FNR{map[$1]=$2} NR>FNR{print $0"\t"map[$1]}' lr_predict_post_count lr_join_ctr_statistics2_with_src_post_count > lr_join_ctr_statistics2_with_src_lr_post_count
awk -F "\t" 'NR==FNR{map[$1]=$2} NR>FNR{print $0"\t"map[$1]}' ctr_predict_post_count lr_join_ctr_statistics2_with_src_lr_post_count > lr_join_ctr_statistics2_with_src_lr_ctr_post_count
# 查看ctr_predict_post_count第二列的最大最小值20,1
awk 'NR==1{max=min=$2;next}{max=max>$2?max:$2;min=min<$2?min:$2}END{print max,min}' ctr_predict_post_count

########### 16.取lr_predict前20
#1. 先折叠
awk 'BEGIN{FS=" "} {map[$1]=map[$1]$NF" "} END{for(i in map)print i,map[i]}' lr_predict > lr_predict_tmp
#2. 删除末尾空格
sed 's/[ \t]*$//' lr_predict_tmp > lr_predict_tmp1
#3. 再展开
awk '{for(i = 2; i <= NF && i <= 21; i++) {if(i < 21) {printf "%s\t%s\n",$1,$i} else{print $1"\t"$i}}}' lr_predict_tmp1 > lr_predict_top20
#4. 验证
awk '$1=="1000010000#1001879"{print $0}' lr_predict_top20
#awk '{for(i = 3; i <= NF; i++) {if(i < NF) {printf "%s\t%s\n",$2,$i} else{print $2"\t"$i}}}' test2 > test3


#以第1列为key，统计相同key的行数
awk 'BEGIN{FS="\t"}{a[$1]+=1}END{for(i in a)print  i"\t"a[i]}' file

#统计一列中不同值的个数
awk 'BEGIN{FS="\t"}{a[$1]=1;sum=0} END{for(i in a) sum+=a[i];print sum}' file

#打印第1列等于指定key的记录个数
awk '$1=="700110000#1225074"{print ++i"\t"$0}' file

#合并两个文件
awk -F "\t" 'ARGIND==1{map[$1]=$2;}  ARGIND==2{print $0"\t"map[$1];}' file1 file2
或
awk -F "\t" 'NR==FNR{map[$1]=$2} NR>FNR{print $0"\t"map[$1]}' file1 file2

#将第2列减第3列作为第4列
awk -F "\t" '{map[$1]=$2-$3;if($2-$3>0) map2[$1]=1;if($2-$3<0) map2[$1]=-1;if($2-$3==0) map2[$1]=0} {print $0"\t"map[$1]"\t"map2[$1]}' file

#对每个相同的key取前10,第1列是key，第2列是value
#1. 先折叠
awk 'BEGIN{FS=" "} {map[$1]=map[$1]$NF" "} END{for(i in map)print i,map[i]}' file > tmp
#2. 然后删除末尾空格
sed 's/[ \t]*$//' tmp > tmp1
#3. 最后还原展现前20
awk '{for(i = 2; i <= NF && i <= 21; i++) {if(i < 21) {printf "%s\t%s\n",$1,$i} else{print $1"\t"$i}}}' tmp1 > output

# 取第2列的最小值，最大值
awk 'NR==1{max=min=$2;next}{max=max>$2?max:$2;min=min<$2?min:$2}END{print max,min}'

# 两个文件获取相同的记录
awk 'NR==FNR{a[$0]++} NR>FNR&&a[$0]' file1 file2
#rm tmp tmp1 tmp2 tmp3

# 对每个key取前四
awk -F "\t" '
BEGIN{last="";}
{
    if(!($1 in map))
    {
        print$0; map[$1]=1;
    }
    else
    {
        map[$1]=map[$1]+1;
        if(map[$1]<5)
        {
            print $0;
        }
    }
}
' $1

## 对某一列求和
awk '{sum += $1};END {print sum}' test
