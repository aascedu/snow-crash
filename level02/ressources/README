There is a .pcap file.
After a quick internet search, we know that it is a packet capture file.
So we open wireshark and see the data.
Since there are so few packets, when we look at all of them, we can see one containing data 'Password:'
Also we noticed it is a plaintext communication.
We can follow the TCP Stream to look at the transfer as a whole

We get this :
..%
..%
..&..... ..#..'..$
..&..... ..#..'..$
.. .....#.....'.........
.. .38400,38400....#.SodaCan:0....'..DISPLAY.SodaCan:0......xterm..
........"........!
........"..".....b........b....	B.
..............................1.......!
.."....
.."....
..!..........."
........"
..".............	..
.....................
Linux 2.6.38-8-generic-pae (::ffff:10.1.1.2) (pts/10)

..wwwbugs login: 
l
.l
e
.e
v
.v
e
.e
l
.l
X
.X


..
Password: 
ft_wandr...NDRel.L0L

.
..
Login incorrect
wwwbugs login: 


When we input the password when doing su flag02 and pasting ft_wandr...NDRel.L0L it is not working. So I looked at the data in a C array format.
We find packets with 0x7f which is not the value for '.' char, with a quick search online, we find it is the value for DEL key.
So we know that the whole password has extra char in it.
