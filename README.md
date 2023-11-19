// contact-management-system
//using c



#include<stdio.h>
#include<string.h>
#include<stdlib.h>
struct node *root=NULL;
struct node 
{
    char name[20];
    char no[20];
    struct node *link;
};
void insert()
{struct node *temp;
    struct node *temp1;
    struct node *temp2;
    temp=(struct node *)malloc(sizeof(struct node));
    temp->link=NULL;
    printf("GIVE THE NAME OF THE PERSON:");
    scanf("%s",temp->name);
    printf("GIVE THE PHONE NUMBER OF THE PERSON:");
    scanf("%s",temp->no);
    if(root==NULL)
    {
        root=temp;
    }
    else if(strcmp(root->name,temp->name)>0)
    {
       temp->link=root;
       root=temp;
    }
    else
    {
        temp1=NULL;
        for(temp2=root;temp2!= NULL && strcmp(temp->name,temp2->name)>0;temp2=temp2->link)
        {
            temp1=temp2;
        }
        temp1->link=temp;
        temp->link=temp2;
    }
}
void display()
{
    struct node *t;
    t=root;
    int i=1;
    printf("S.no         NAME                    PHONE.NO\n");
    while(t!=NULL)
    {
        printf("%d             %-25s%s\n",i,t->name,t->no);
        i=i+1;
        t=t->link;
    }
}
void delete()
{
    char d[20];
    printf("GIVE THE VALID CONTACT U WANT TO DELETE:");
    scanf("%s",d);
    struct node *temp1=root;
    struct node *temp2=root;
    if(root==NULL)
    {
        printf("NO CONTACTS\n");
    }
    else if(strcmp(d,temp1->name)==0)
    {
        root=temp1->link;
    }
    else
    {
        temp1=temp1->link;
        while(strcmp(temp1->name,d)!=0)
        {
            temp2=temp2->link;
            temp1=temp1->link;
        }
        temp2->link=temp1->link;
    }
    
}

void search()
{
    char s[10];
    printf("GIVE THE STR U WANT TO SEARCH:");
    scanf("%s",s);
    struct node *temp;
    temp=root;
    while(temp!=NULL)
    {
        if(strcmp(s,temp->name)==0)
        {
            printf("NAME:%s,PHONE.NO:%s\n",temp->name,temp->no);
        }
        temp=temp->link;
    }
}
int main()
{
    printf("FOR ADDING CONTACT KEY=>1\n");
    printf("FOR DELETING CONTACT KEY=>2\n");
    printf("FOR display specific CONTACT KEY=>3\n");
    printf("FOR DISPLAYING ALL CONTACTS KEY=>4\n");
    printf("FOR EXIT KEY=>5\n");
    int key;
    while (1)
    {
        printf("give the value of key according to the operation:");
        scanf("%d",&key);
        switch(key)
        {
            case 1:
                insert();
                break;
            case 2:
                delete();
                break;
            case 3:
                search();
                break;
            case 4:
                display();
                break;
            case 5:
                return 0;
            default:
                printf("give the key as in above range\n");
        }
    }
    return 0;
}
