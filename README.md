#include<iostream>
using namespace std;
struct node
{
    int data;
   node *next;
};
node * start=nullptr;
int menu()
{
    int ch;
    cout<<"1.create a list"<<endl;
    cout<<"--------------"<<endl;
    cout<<"2.inset a node at specified position"<<endl;
    cout<<"-------------------"<<endl;
    cout<<"3.Display"<<endl;
    cout<<"--------------------"<<endl;
    cout<<"4.exit"<<endl;
    cout<<"------------------------"<<endl;
    cout<<"enter your choice:"<<endl;
    cin>>ch;
    return ch;
}
node * getnode()
{
      node * newnode=new node();
    cout<<"enter data:"<<endl;
    cin>>newnode->data;
    newnode->next=nullptr;
    return newnode;

}
void createlist(int n)
{
    for(int i=0;i<n;i++)
    {
        node * newnode=getnode();
        if(start==nullptr)
        {
            start=newnode;
        }
        else
        {


            node * temp=start;
            while(temp->next!=nullptr)
            {
                temp=temp->next;
            }
            temp->next=newnode;
        }
    }
}
int countnode(node*ptr)
{
    int count=0;
    while(ptr!=nullptr)
    {
        ++count;
        ptr=ptr->next;
    }
    return count;
}
void display()
{
    node * temp=start;
    cout<<"The contents of the list(left to right):"<<endl;
    if(start==nullptr)
    {
        cout<<"empty list"<<endl;
    }
    else
    {
        while(temp!=nullptr)
        {
            cout<<temp->data;
            temp=temp->next;
        }
    }
    cout<<"X";
}
void insertatpos()
{
    node * newnode=getnode();
    int pos,nodecount;
    cout<<"enter the position"<<endl;
    cin>>pos;
    nodecount=countnode(start);
    if(pos<1 || pos>nodecount+1)
    {
        cout<<"position "<<pos<<"is invalid"<<endl;
        delete newnode;
        return;
    }
    if(pos==1)
    {
        newnode->next=start;
        start=newnode;
    }
    else
    {
        node * temp=start;
        for(int i=0;i<pos;i++)
        {
            temp=temp->next;


        }
        newnode->next=temp->next;
        temp->next=newnode;
    }
}
int main()
{
    int ch;
    int n;
    while(true)
    {
        ch=menu();
        switch(ch)
        {
        case 1:
            if(start==nullptr)
            {
                cout<<"number of nodes u want to create;";
                cin>>n;
                createlist(n);
                cout<<"list is created"<<endl;
            }
            else
            {
                cout<<"list is already creatd"<<endl;
            }
            break;
        case 2:
            insertatpos();
            break;
        case 3:
            display();
            break;
        case 4:
            exit(0);
        default:
            cout<<"Invalid choice"<<endl;
        }
    }

    return 0;
}


//poisonous plant
#include <iostream>
#include<vector>
#include<stack>
#include<algorithm>
using namespace std;
struct plant
{
    int pesticide;
    int days ;
};
int poisonousplants(int n,vector<int>& p)
{
    stack<plant> s;
    int max_days=0;
    for(int i=0;i<n;i++)
    {
        int days=0;
        while(!s.empty() && s.top().pesticide>=p[i])
        {
            days=max(days,s.top().days);
            s.pop();
        }
        if(!s.empty())//plant with low pesticide level is there in the loop
        {
            days++;
        }
        else
        {

            days=0;
        }
        max_days=max(max_days,days);
        s.push({p[i],days});
       
    }
     return max_days;//got error here check;

}
int main()
{
    int n;
    cout<<"enter the number of plants:"<<endl;
    cin>>n;
    vector <int> p(n);

    cout<<"enter the pesticide levels for each plant"<<endl;
    for(int i=0;i<n;i++)
    {
        cin>>p[i];
    }
    int result=poisonousplants(n,p);
cout<<result;

    return 0;
}


#include<iostream>
#include<vector>
using namespace std;
int main()
{
    int n;
    cout<<"Enter the number of petrol stations:"<<endl;
    cin>>n;
    vector<int> p(n);
    vector<int> d(n);
    cout<<"enter the petrol and the distance"<<endl;
    for(int i=0;i<n;i++)
    {
        cin>>p[i]>>d[i];
    }
    int start=0,deficiet=0,capacity=0;
    for(int i=0;i<n;i++)
    {
        capacity+=p[i]-d[i];//don't forget to add += here then u get wrong

        if(capacity<0)
        {
            start=i+1;
            deficiet=deficiet+capacity;
            capacity=0;
        }
    }
    if(capacity+deficiet>=0)
    {
        cout<<start<<endl;
    }
    else
    {
        cout<<-1<<endl;
    }
    return 0;
}


#include <iostream>
using namespace std;
struct node
{
    int data;
    node* left;
    node* right;
    node(int val)
    {
        data=val;
        left=nullptr;
        right=nullptr;
    }
};
int height(node* node)
{
    if(node==nullptr)
    {
        return 0;
    }
    int leftheight=height(node->left);
    int rightheight=height(node->right);
    return  max(leftheight,rightheight)+1;
}
int main()
{
   node* root=new node(10);
   root->left=new node(20);
   root->right=new node(30);
   root->left->left=new node(40);
   root->left->right=new node(50);
   cout<<"Heigth of the tree is:"<<height(root)<<endl;
    return 0;
}



#include<iostream>
using namespace std;
struct node
{
    int data;
    node* left;
    node* right;
    node (int val)
    {
        data=val;
        left=nullptr;
        right=nullptr;
    }
};
node* lca(node* root , int n1,int n2)
{
    while(root!=nullptr)
    {
        if(root->data>n1 && root->data>n2)
        {
            root=root->left;
        }
        else if(root->data < n1 && root->data < n2)
        {
            root=root->right;
        }
        else
            break;
    }
    return root;
}
int main()
{
    node* root=new node(20);
    root->left=new node(8);
    root->right=new node(22);
    root->left->left=new node(4);
    root->left->right=new node(12);
    root->left->right->left=new node(10);
    root->left->right->right=new node(14);
    int n1=10,n2=14;
    node* t=lca(root,n1,n2);
    cout<<"lca of"<<n1<<"and"<<n2<<"is:"<<t->data<<endl;
    return 0;
}






























































