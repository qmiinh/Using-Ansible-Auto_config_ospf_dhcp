
# Hướng dẫn sử dụng Ansible tự động cấu hình OSPF, DHCP

  LAB sử dụng:
  - GNS3 2.1.5
- IOS image: c7200-adventerprisek9-mz.124-15.T9.image
- Centos 7
- Ansible 2.7.5
# Phụ lục

  

[A. Thông tin LAB](#a)

[A. Các bước thực hiện](#b)

<a name="a"></a>
## A. Thông tin LAB

### A.1 Topo

![Alt text](https://i.imgur.com/2D9Hffk.png)

### A.2 IP
  Cấu hình địa chỉ IP theo thông số sau:
<table>
  <tr>
    <th>Hostname</th>
    <th>Interface</th>
    <th>IP ADDRESS</th>
    <th>SUBNET MASK</th>
    <th>GATEWAY</th>
  </tr>
   <tr>
    <td rowspan="1"> ComputeNode</td>
    <td></td>
    <td>88.0.0.7</td>
    <td>255.255.255.0</td>
    <td>88.0.0.1</td>
    <td> </td>
  </tr>
  <tr>
    <td rowspan="3"> Router1</td>
    <td>F 2/0</td>
    <td>88.0.0.11</td>
    <td>255.255.255.0</td>
    <td> </td>
    <td> </td>
  </tr>
  <tr>
    <td>F 0/0</td>
    <td>192.168.12.1</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
    <td>F 1/0</td>
    <td>192.168.1.1</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
    <td rowspan="4"> Router2</td>
    <td>F 3/0</td>
    <td>88.0.0.22</td>
    <td>255.255.255.0</td>
    <td> </td>
    <td> </td>
  </tr>
  <tr>
    <td>F 0/0</td>
    <td>192.168.12.2</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
    <td>F 1/0</td>
    <td>192.168.23.2</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
    <td>F 2/0</td>
    <td>192.168.2.1</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
    <td rowspan="3"> Router3</td>
    <td>F 2/0</td>
    <td>88.0.0.33</td>
    <td>255.255.255.0</td>
    <td> </td>
    <td> </td>
  </tr>
  <tr>
    <td>F 0/0</td>
    <td>192.168.23.3</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
    <td>F 1/0</td>
    <td>192.168.3.1</td>
    <td>255.255.255.0</td>
    <td></td>
    <td></td>
  </tr>
    <tr>
</table>


Sau khi cấp các máy tính nhận DHCP, kết quả mong muốn:
<table>
  <tr>
    <th>Hostname</th>
    <th>IP ADDRESS</th>
    <th>SUBNET MASK</th>
    <th>GATEWAY</th>
    <th>DNS</th>
  </tr>
   <tr>
    <td rowspan="1"> PC1</td>
    <td>Dynamic</td>
    <td>255.255.255.0</td>
    <td>192.168.1.1</td>
    <td>8.8.8.8</td>
  </tr>
    </tr>
   <tr>
    <td rowspan="1"> PC2</td>
    <td>Dynamic</td>
    <td>255.255.255.0</td>
    <td>192.168.2.1</td>
    <td>8.8.8.8</td>
  </tr>
    </tr>
   <tr>
    <td rowspan="1"> PC3</td>
    <td>Dynamic</td>
    <td>255.255.255.0</td>
    <td>192.168.3.1</td>
    <td>8.8.8.8</td>
  </tr>
  </table>
  
  <a name="b"></a>
## B. Các bước thực hiện
  
### B.1 Cấu hình kết nối tới Controller Node

- Cấu hình đặt IP Router sao cho kết nối thành công tới Controller Node qua dải Manager Network.
- Cấu hình SSH để Ansible có thể kết nối SSH tới các host.

### B.2 Sử dụng Ansible để cấu hình
- Đặt tên, đặt Ip cho R1 R2 R3.
- Định tuyến OSPF.
- Cấu hình DHCP pool trên R1 R2 R3, cấp phát IP cho PC1, PC2, PC3.
- Ping từ PC1 đến các PC khác thành công


