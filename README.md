# Stack_data_structure
import java.util.*;
public class Stack_alpha {
    //1.Stack using ArrayList

    static class stack {
        /*
       static ArrayList<Integer>list = new ArrayList<>();
       //empty
       public static boolean isEmpty()
       {
           return list.size() == 0;
       }
       //push
       public static void push(int data)
       {
           list.add(data);
       }
       //pop
       public static int pop()
       {
           if(isEmpty())
           {
               return -1;
           }
           int top = list.get(list.size()-1);
           list.remove(list.size()-1);
           return top;
       }
       //peek
       public static int peek()
       {
           if(isEmpty())
           {
               return -1;
           }
           return list.get(list.size()-1);
       }

    }

    */


        //2.stack using LinkedList
    /*
    static class Node
    {
        int data;
        Node next;
        Node(int data)
        {
            this.data = data;
            this.next = null;
        }
    }
    static class stack
    {
        static Node head = null;
        public static boolean isEmpty()
        {
            return head == null;
        }
        //push
        public static void push(int data)
        {
            Node newNode = new Node(data);
            if(isEmpty())
            {
                head = newNode;
                return;
            }
            newNode.next = head;
            head = newNode;
        }
        //pop
        public static int pop()
        {
            if(isEmpty())
            {
                return -1;
            }
            int top = head.data;
            head = head.next;
            return top;
        }
        //peek
        public static int peek()
        {
            if(isEmpty())
            {
                return -1;
            }
            return head.data;
        }

    }



    public static void main(String args[])
    {
        //same for 1 & 2
         stack s= new stack();
         s.push(1);
        s.push(2);
        s.push(3);
        while(!s.isEmpty())
        {
            System.out.println(s.peek());
            s.pop();
        }
    }




        //3.Stack using Collection framework
        public static void main(String args[]) {
            Stack<Integer> s=new Stack<>();
            s.push(1);
            s.push(2);
            s.push(3);
            while (!s.isEmpty()) {
                System.out.println(s.peek());
                s.pop();
            }
        }




        //4.Duplicate parentheses
        public static boolean isDuplicate(String str)
        {
            Stack<Character>s=new Stack<>();
            for(int i=0;i<str.length();i++)
            {
               char ch = str.charAt(i);
               //closing
                if(ch==')')
                {
                    int count =0;
                    while(s.peek() != '(')
                    {
                        s.pop();
                        count++;
                    }
                    if(count<1)
                    {
                        return true; //duplicate
                    }
                    else
                    {
                        s.pop();   //opening pair
                    }
                }
                else
                {
                    //opening
                    s.push(ch);
                }
            }
            return false;
        }
        public static void main(String args[])
        {
            String str1 = "((a+b))";  //true
            String str2 = "(a-b)";   //false
            System.out.println(isDuplicate(str2));
        }

     */




        //5 Max area in Histogram
        public static void maxArea(int arr[])
        {
            int maxArea = 0;
            int nsr[] = new int[arr.length];
            int nsl[] = new int[arr.length];

            //Next smaller right
            Stack<Integer>s=new Stack<>();
            for(int i=arr.length-1;i>=0;i--)
            {
                while(!s.isEmpty() && arr[s.peek()] >= arr[i])
                {
                    s.pop();
                }
                if(s.isEmpty())
                {
                    nsr[i] = arr.length;
                }
                else
                {
                    nsr[i] = s.peek();
                }
                s.push(i);
            }
            //Next smaller left
            s=new Stack<>();
            for(int i=0; i<arr.length;i++)
            {
                while(!s.isEmpty() && arr[s.peek()] >= arr[i])
                {
                    s.pop();
                }
                if(s.isEmpty())
                {
                    nsl[i] = -1;
                }
                else
                {
                    nsl[i] = s.peek();
                }
                s.push(i);
            }
            //Current area
            for(int i=0;i<arr.length;i++)
            {
                int height = arr[i];
                int width = nsr[i] - nsl[i]-1;
                int currArea = height * width;
                maxArea = Math.max(currArea ,maxArea);
            }
            System.out.println("max area in histogram = " + maxArea);
        }
        public static void main(String args[])
        {
            int arr[] = {2,1,5,6,2,3};
            maxArea(arr);
        }
    }



}
