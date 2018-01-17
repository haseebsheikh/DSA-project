# DSA-project
Interpollation Search using recursion and filling(for INPUT and OUTPUT)

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text.RegularExpressions;
using System.IO;

namespace Rextester
{
    public class Program
    {
        public static int interpolationSearch(int[] arr, int x,int pos,int lo,int hi)
        {            
            // Since array is sorted, an element present
            // in array must be in range defined by corner
            if(lo <= hi && x >= arr[lo] && x <= arr[hi])
            {
                // Probing the position with keeping
                // uniform distribution in mind.
                pos = lo + (int)(((double)(hi-lo)/(arr[hi]-arr[lo]))*(x - arr[lo]));
                // Condition of target found
                if (arr[pos] == x)
                    return pos;
                // If x is larger, x is in upper part
                if (arr[pos] < x)
                    lo = pos + 1;
                // If x is smaller, x is in lower part
                else
                    hi = pos - 1;
                interpolationSearch(arr,x,pos,lo,hi);                                                                
            }
            return -1;    
        }
        //function to read input from text(Elements of an array)
        public static int[] readFile(string path,int[] arr) 
        {
            int i=0;           
            using(StreamReader sr=new StreamReader(path)) 
            { 
                String read;  
                while((read=sr.ReadLine())!=null) 
                { 
                     arr[i]=Convert.ToInt32(read);  
                     i++; 
                } 
            } 
            return arr;  
        }
        //function to write result
        public static void outputFile(string path,int index)
        {
            if (index != -1)
                using(StreamWriter outputFile=new StreamWriter(path))
                {
                     outputFile.WriteLine("Element found at index" + index);
                }
                
            else
                using (StreamWriter outputFile = new StreamWriter(path))
                {
                    outputFile.WriteLine("Element not found.");
                }            
        }             

        public static void Main(string[] args)
        {
            // Array of items on which search will
            // be conducted.            
            int[] arr=new int[5];
            
            Console.WriteLine("Enter the element to search");
            int x = Convert.ToInt32(Console.ReadLine()); // Element to be searched  
            
            arr=readFile("C:\\Users\\Haseeb\\Desktop\\input.txt");
            int index = interpolationSearch(arr, x,0,0,arr.Length-1);
            
            outputFile(string path,int index);                        
        }
    }
}
