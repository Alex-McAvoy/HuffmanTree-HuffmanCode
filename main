#include<iostream>
#include<cstdio>
#include<cstdlib>
#include<string>
#include<cstring>
#include<cmath>
#include<ctime>
#include<algorithm>
#include<utility>
#include<stack>
#include<queue>
#include<vector>
#include<set>
#include<map>
#include<bitset>
#define EPS 1e-9
#define PI acos(-1.0)
#define INF 0x3f3f3f3f
#define LL long long
const int MOD = 1E9+7;
const int N = 100+5;
const int dx[] = {-1,1,0,0,-1,-1,1,1};
const int dy[] = {0,0,-1,1,-1,1,-1,1};
using namespace std;
struct Node{
    int weight;
    Node *lchild,*rchild;
};
typedef Node *tree;
tree create(int arr[],int n){
    tree forest[N];
    tree root=NULL;
    for (int i=0; i<n; i++){//将所有点存入森林
        tree temp;
        temp=(tree)malloc(sizeof(Node));
        temp->weight = arr[i];
        temp->lchild = temp->rchild = NULL;
        forest[i]=temp;
    }

    for(int i=1; i<n; i++) {//n-1次循环建哈夫曼树
        int minn=-1,minnSub;//minn为最小值树根下标,minnsub为次小值树根下标
        for(int j=0; j<n; j++) {
            if (forest[j]!=NULL && minn==-1) {
                minn=j;
                continue;
            }
            if (forest[j]!=NULL) {
                minnSub=j;
                break;
            }
        }

        for (int j=minnSub; j<n; j++){//根据minn与minnSub赋值
            if(forest[j]!=NULL){
                if(forest[j]->weight < forest[minn]->weight){
                    minnSub=minn;
                    minn=j;
                }
                else if(forest[j]->weight < forest[minnSub]->weight){
                    minnSub=j;
                }
            }
        }

        //建新树
        root = (tree)malloc(sizeof(Node));
        root->weight = forest[minn]->weight + forest[minnSub]->weight;
        root->lchild = forest[minn];
        root->rchild = forest[minnSub];

        forest[minn]=root;//指向新树的指针赋给minn位置
        forest[minnSub]=NULL;//minnSub位置为空
    }
    return root;
}
int getWPL(tree &root,int len){//计算哈夫曼树带权路径长度WPL
    if(root==NULL)
        return 0;
    else {
        if(root->lchild==NULL&&root->rchild==NULL)//叶节点
            return root->weight*len;
        else
            return getWPL(root->lchild,len+1)+getWPL(root->rchild,len+1);
    }
}
void HuffmanCoding(tree &root,int len,int arr[]){//哈夫曼树编码
    if(root!=NULL){
        if(root->lchild==NULL&&root->rchild==NULL){
           printf("结点为%d的字符的编码为: ",root->weight);
           for(int i=0;i<len;i++)
               printf("%d", arr[i]);
           printf("\n");
        }
        else{
            arr[len]=0;
            HuffmanCoding(root->lchild,len+1,arr);
            arr[len]=1;
            HuffmanCoding(root->rchild,len+1,arr);
        }
    }
}
int main(){
    int n=6;//长度
    int arr[]={3,9,5,12,6,15};//权值
    tree root=create(arr,n);

    int WPL=getWPL(root,0);
    printf("WPL=%d\n",WPL);

    printf("==========各节点的哈夫曼树编码==========\n");
    HuffmanCoding(root,0,arr);

    return 0;
}
