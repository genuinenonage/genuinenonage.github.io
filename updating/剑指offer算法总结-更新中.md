---
title: 剑指offer算法总结
date: 2020/08/20 19:47:00
tags: 
- 算法
- offer
categories:
- 算法
---
## 03. 数组中重复的数字 
利用集合的唯一性。

	//重要代码
	Set<Integer> set = new HashSet<Integer>();
	set.add(value)  


* 集合中没有返回true
* 集合中已存在，返回false   

		public int findRepeatNumber(int[] nums) {  
			Set<Integer> set = new HashSet<Integer>();  
			for(int num: nums){  
				if(!set.add(num)){  
					return num;
				}
			}
			return -1;
		}


## 04. 二维数组中的查找  
标签：数组，双指针  
利用题目的特性，找出解题的简便方法，使程序流程变得简单。  
    
	class Solution {
	    int tar = 0;
	    int n = 0;
	    int m = 0;
	    public boolean findNumberIn2DArray(int[][] matrix, int target) {
	        tar=target;
	        n = matrix.length;
	        if(n == 0){
	            return false;
	        }
	        m = matrix[0].length;
	        if(m == 0){
	            return false;
	        }
	        return bianli(matrix,0,m-1);
	    }
	
	    public boolean bianli(int[][] numss, int i, int j){
	        if(numss[i][j] < tar && i+1 < n){
	            return bianli(numss, i+1, j);
	        }else if(numss[i][j] == tar){
	            return true;
	        }else if( j-1>=0){
	            return bianli(numss,i,j-1);
	        }
	        return false;
	    }
	}

## 05. 替换空格   
字符数组的使用比字符串拼接（+）快无数倍。  

	//重要代码  
	String s = new String(chars, 0, size);

	class Solution {
	    public String replaceSpace(String s) {
	        int len = s.length();
	        char[] chars = new char[len * 3];
	        int size = 0;
	        for(int i = 0; i < len; i++){
	            char c = s.charAt(i);
	            if(c == ' '){
	                chars[size++] = '%';
	                chars[size++] = '2';
	                chars[size++] = '0';
	            }else{
	                chars[size++] = c;
	            }
	        }
	        String res = new String(chars, 0, size);
	        return res;
	    }
	}  

## 06. 从尾到头打印链表-未完成  
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。  

	class Solution {
	    public int[] reversePrint(ListNode head) {
	        //1. 首先使用数组解决 效率高内存占用低
	        int[] arr = new int[10000];
	        int size = 0;
	        while(head!= null){
	            arr[size] = head.val;
	            size ++;
	            head = head.next;
	        }
	        int [] rearr = new int[size];
	        int i = 0;
	        int j = 0;
	        for(i = size-1,j = 0;i >= 0;i --,j++){
	            rearr[i] = arr[j];
	        }
	        return rearr;
	
	        //2. 使用栈解决 效率低内存占用高
	        // Stack<Integer> stack = new Stack<Integer>();
	        // while(head != null){
	        //     stack.push(head.val);
	        //     head = head.next;
	        // }
	        // int size = stack.size();
	        // int[] rearr = new int[size];
	        // for(int i = 0; i < size; i++){
	        //     rearr[i] = stack.pop();
	        // }
	        // return rearr;
	    }
	}

## 10- I. 斐波那契数列  
输入 n ，求斐波那契（Fibonacci）数列的第 n 项。    
答案需要取模 1e9+7（1000000007）。    

	int constant = 1000000007;
    Map<Integer,Integer> map = new HashMap();
    public int fib(int n) {
        // return digui(n);
        return nodigui(n);
    }
    //递归
    // public int digui(int n) {
    //     if (n < 2)
    //         return n;
    //     if (map.containsKey(n))
    //         return map.get(n);
    //     int first = digui(n - 1) % constant;
    //     map.put(n - 1, first);
    //     int second = digui(n - 2) % constant;
    //     map.put(n - 2, second);
    //     int res = (first + second) % constant;
    //     map.put(n, res);
    //     return res;
    // }
    //非递归
    public int nodigui(int n){
        int one = 0;
        int two = 1;
        int res = 0;
        while(n-- > 0){
            res = (one+two)%constant;
            one = two%constant;
            two = res;
        }
        return one;
    }






