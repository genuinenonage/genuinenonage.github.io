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
利用题目的特性，找出解题的简便方法，是程序流程变得简单。  
    
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
	        ListNode start = new ListNode();
	        start.next = head;
	        ListNode after = new ListNode();
	        int size = 1;
	        where(head.next!=null){
	            size++;
	            head = head.next;
	            temp = head;
	            after = start.next;
	            start.next = temp;
	            temp.next = after;
	        }
	        int 
	        where(start.next!=null){
	            
	        }
	    }
	}





