您可以在负载均衡实例上添加一个 UDP 监听器转发来自客户端的 UDP 协议请求。UDP 协议适用于对传输效率要求高、对准确性要求相对较低的场景，如即时通讯、在线视频等。UDP 协议的监听器，后端服务器可直接获取客户端的真实 IP。

## 限制说明
UDP 监听器的4789端口为系统保留端口，暂不对外开放。



## 前提条件
您需要 [创建负载均衡实例](https://cloud.tencent.com/document/product/214/6149)。

## 操作步骤
### 步骤一：配置监听器
1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb)，在左侧导航栏单击**实例管理**。
2. 在 CLB 实例列表页面左上角选择地域，在实例列表右侧的操作列中单击**配置监听器**。
![](https://qcloudimg.tencent-cloud.cn/raw/2c0b7f73cd81582c7ace11dbfe7d6c18.png)
3. 在 TCP/UDP/TCP SSL/QUIC 监听器下，单击**新建**，在弹出的“创建监听器”对话框中配置 UDP 监听器。
 **a. 基本配置**
<table>
<thead>
<tr>
<th width="15%">监听器基本配置</th>
<th width="70%">说明</th>
<th width="15%">示例</th>
</tr>
</thead>
<tbody><tr>
<td>名称</td>
<td>监听器的名称。</td>
<td><span>test-udp-8000 &nbsp; &nbsp; &nbsp;</span></td>
</tr>
<tr>
<td>监听协议端口</td>
<td><ul><li>监听协议：本示例选择 UDP。</li><li>监听端口：用来接收请求并向后端服务器转发请求的端口，端口范围为1 - 65535，其中4789端口为系统保留端口，暂不对外开放。</li><li> 同一个负载均衡实例内，监听端口不可重复。</li></ul></td>
<td>UDP:8000</td>
</tr>
<tr>
<td>均衡方式</td>
<td>UDP 监听器中，负载均衡支持加权轮询（WRR）和加权最小连接数（WLC）两种调度算法。 <br/> <ul><li>加权轮询算法：根据后端服务器的权重，按依次将请求分发给不同的服务器。加权轮询算法根据<strong>新建连接数</strong>来调度，权值高的服务器被轮询到的次数（概率）越高，相同权值的服务器处理相同数目的连接数。</li><li> 加权最小连接数：根据服务器当前活跃的连接数来估计服务器的负载情况，加权最小连接数根据服务器负载和权重来综合调度，当权重值相同时，当前连接数越小的后端服务器被轮询到的次数（概率）也越高。</li></ul>
<dx-alert infotype="explain" title="">
选取加权最小连接数的均衡方式后，监听器不支持开启会话保持功能。
</dx-alert>
</td>
<td>加权轮询</td>
</tr>
<tr>
<td>按 QUIC ID 调度</td>
<td>启用后，CLB 将按 QUIC ID 来调度，相同的 QUIC Connection ID 会调度到相同的后端服务器。如果客户端请求没有包含 QUIC Connection ID，则降级到普通加权轮询，即按四元组（源 IP+目的 IP+源端口+目的端口）进行调度。</td>
<td><span>开启</span></td>
</tr>
</tbody></table>
 <b>b. 健康检查</b></br>
健康检查详情请参见<a href="https://cloud.tencent.com/document/product/214/50011#udp"> UDP 健康检查</a>。</br>
 <b>c. 会话保持</b>
<table>
<tr>
<th width="15%">会话保持配置</th>
<th width="70%">说明</th>
<th width="15%">示例</th>
</tr>
<tr>
<td width="15%">会话保持开关</td>
<td width="70%"><ul><li>开启会话保持后，负载均衡监听会把来自同一客户端的访问请求分发到同一台后端服务器上。</li><li>TCP 协议是基于客户端 IP 地址的会话保持，即来自同一 IP 地址的访问请求转发到同一台后端服务器上。</li><li>加权轮询调度支持会话保持，加权最小连接数调度不支持开启会话保持功能。</li></ul></td>
<td width="15%">开启</td>
</tr>
<tr>
<td width="15%">会话保持时间</td>
<td width="70%">会话保持时间<br><ul><li>当超过保持时间，连接内无新的请求，将会自动断开会话保持。</li><li>可配置范围30 - 3600秒。</li></ul></td>
<td width="15%">30s</td>
</tr>
</table>

### 步骤二：绑定后端云服务器
1. 在“监听器管理”页面，单击刚才创建的监听器，如上述 `UDP:8000` 监听器，即可在监听器右侧查看已绑定的后端服务。
2. 单击**绑定**，在弹出框中选择需绑定的后端服务器，并配置服务端口和权重。
>? 默认端口功能：先填写“默认端口”，再选择云服务器后，每台云服务器的端口均为默认端口。


### 步骤三：安全组（可选）
您可以配置负载均衡的安全组来进行公网流量的隔离，详情请参见 [配置负载均衡安全组](https://cloud.tencent.com/document/product/214/14733)。

### 步骤四：修改/删除监听器（可选）
如果您需要修改或删除已创建的监听器，请在“监听器管理”页面，单击已创建完毕的监听器，单击![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg)图标修改或![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg)图标删除。



