<h2>Big Files</h2>
<pre>
  <code>
    DNINDIRECT = total number of blocks in doubly indirect blocks

param.h
	- increase FSSIZE to 200000

fs.h
	- change the size of NDIRECT to 11
	- dinode
		- addrs[NDIRECT+2]


file.h
	- inode
		- addrs[NDIRECT+2]

fs.c

bmap:
	- block no. - 256, so that it aligns with doubly blocks list 
	- if (check if block no. is < DNINDIRECT)
		- if (addrs[13] == exists )
			- if not than balloc to get a new block from memory
				- check if ballock was successful
					- if not return 0
				- assign the new address to inode->addrs[13]
		- read from the buffer to get the buffer was the addrs[13]
		- to get the index in of the block in the middle layer 
			- middleBlock =  block no. / 256, integer division
		- if(bufferData[middleBlock]==0)
			- balloc for new block
			- if balloc sucess
				- bufferData[middleBlock] = newly allocated block;
				- And write to the log
			- dont forget to release the buffer lock
      - get the buffer for the block in second layer, which will give us access
		to the last layer
		- to get the index for last layer block number % 256
		- if bufferdata[block]
			- doent exist than balloc
			- assign it to the buffer
			and log write
		- return the last block

itrunc:
  - check if the 13th block exists
		- if does
			- get bufferData[12]
		  - for (through the middle layer given by bufferData[12])
				- get buffer for each bufferData[i]
				- for  bufferData[i]
					- loop through to get to the last layer
					- free each block
				- free the block in middle layer
				- set the address to 0
			- free the DNINDIRECT block
			- set its address ti 0
					


    
  </code>
</pre>
