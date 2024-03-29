# MaxRetangleInPolygon
### Description
利用方格划分求多边形内接最大面积的矩形
### 源码
**main.cpp**
```
#include<iostream>
#include<vector>
#include <algorithm>
using namespace std;
typedef struct pt{
    int x;
    int y;
    pt(int xInit,int yInit):x(xInit),y(yInit){};
}Pt;

int MaxmalRetangle(int arr[][8],int m,int n,Pt &leftupper,Pt &rightlower)
{
    int MaxRetan=INT_MIN;
    for (int i = 0; i < m; ++i)
    {
        for (int j = 0; j < n; ++j)
        {
            if(arr[i][j] == 0)
                continue;
            int len=1;
            for(int k=j+1;k<n;k++)
            {
                if(arr[i][k] !=1)
                    break;
                len++;
            }
            int minwid;
            vector<int>candidateMinWid;
            for(int k=j+len-1;k>=j;k--)
            {
                int tempwid=0;
                for (int l = i; l < m; ++l) {
                    if(arr[l][k] != 1)
                        break;
                    tempwid++;
                }
                candidateMinWid.push_back(tempwid);
            }
            sort(candidateMinWid.begin(),candidateMinWid.end());
            minwid=candidateMinWid[0];
            if(len*minwid > MaxRetan)
            {
                MaxRetan=len*minwid;
                leftupper.x=i;
                leftupper.y=j;
                rightlower.x=i+len-1;
                rightlower.y=j+minwid-1;
            }

        }
    }
    return MaxRetan;
}

int main(int argc, char const *argv[])
{
    int testRetangle[7][8]={{1,0,0,1,1,0,1,1},
                            {1,1,1,1,1,0,1,1},
                            {1,1,1,0,1,1,1,0},
                            {1,1,0,1,1,1,1,1},
                            {0,0,0,1,1,1,1,0},
                            {0,0,0,1,1,1,1,0},
                            {1,1,1,1,1,0,0,0}};
    Pt leftUpper(0,0);
    Pt rightLower(0,0);
    int maxRetangleArea=MaxmalRetangle(testRetangle,7,8,leftUpper,rightLower);
    std::cout<<maxRetangleArea<<std::endl;
    return 0;
}
```
### 测试
![Test7*8](https://github.com/sulayman-soyir/MaxRetangleInPolygon/blob/master/new%20file/%E6%B5%8B%E8%AF%95.PNG)
