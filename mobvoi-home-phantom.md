---


---

<h2 id="mobvoihome-智能家居接入协议">MobvoiHome 智能家居接入协议</h2>
<h3 id="协议概述">协议概述</h3>
<p>控制示例</p>
<pre><code class="prism language-json">{
  "access_token": "A07F878A875E05BC75A4D854EE59017E",
  "msg_id": "78F5BC6E-1412-4F3A-90B9-E849021371CB",
  "query": "把客厅的空调温度调到24度",
  "task": "public.smarthome",
  "params": {
    "param": [
      {
        "norm_value": "温度",
        "raw_data": "温度"
      }
    ],
    "device": [
      {
        "norm_value": "空调",
        "raw_data": "空调"
      }
    ],
    "attr": [
      {
        "norm_value": "客厅",
        "raw_data": "客厅"
      }
    ],
    "value": [
      {
        "norm_value": "24",
        "raw_data": "24"
      }
    ]
  },
  "traits": {
    "intent": "other"
  }
}
</code></pre>
<p>查询示例</p>
<pre><code class="prism language-json">{
  "access_token": "A07F878A875E05BC75A4D854EE59017E",
  "msg_id": "78F5BC6E-1412-4F3A-90B9-E849021371CB",
  "query": "空调温度多少度",
  "task": "public.smarthome",
  "params": {
    "device": [
      {
        "norm_value": "空调", 
        "raw_data": "空调"
      }
    ], 
    "param": [
      {
        "norm_value": "温度", 
        "raw_data": "温度"
      }
    ]
  }, 
  "traits": {
    "intent": "inquiry"
  }
}
</code></pre>
<p>场景控制示例</p>
<pre><code class="prism language-json">{
  "access_token": "A07F878A875E05BC75A4D854EE59017E",
  "msg_id": "78F5BC6E-1412-4F3A-90B9-E849021371CB",
  "query": "开饭了",
  "task": "smarthome_scene",
  "params": {
  }, 
  "traits": {
    "intent": "scene_dinner"
  }
}
</code></pre>
<h4 id="参数协议">1.1 参数协议</h4>
<h4 id="设备相关语义标签">1.2 设备相关语义标签</h4>
<h4 id="意图">1.3 意图</h4>
<p>intent主要用于区分同一种task下的不同意图，如下
当task=public.smarthome时，表示设备控制和设备状态查询，</p>
<p>当task=smarthome_scene时，表示场景控制，</p>
<h4 id="接口返回">1.4 接口返回</h4>
<pre><code class="prism language-json">{
  "status": "success",  // 成功时返回success，错误返回error并附上err_code和err_msg
  "err_code": 0,
  "err_msg": "123",
  "prompt": "需要音箱tts的话"
}
</code></pre>
<table>
<thead>
<tr>
<th>参数</th>
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td>access_token</td>
<td>String</td>
<td>用户的唯一标识，由第三方通过OAuth接口提供</td>
</tr>
<tr>
<td>msg_id</td>
<td>String</td>
<td>请求唯一标示，用于追踪</td>
</tr>
<tr>
<td>query</td>
<td>String</td>
<td>用户说的指令</td>
</tr>
<tr>
<td>task</td>
<td>String</td>
<td>分类，控制类值为public.smarthome，场景类值为 smarthome_scene</td>
</tr>
<tr>
<td>params</td>
<td>Object</td>
<td>对用户说的指令处理之后的nlu结果, key对应语义标签，详见1.2，value对应一个List of Param结构</td>
</tr>
<tr>
<td>Param.raw_value</td>
<td>String</td>
<td>用户说的指令中属于该语义标签的词</td>
</tr>
<tr>
<td>Param.norm_value</td>
<td>String</td>
<td>用户说的指令中属于该语义标签的词标准化的结果，比如用户说的“风扇”，这里会被标准化到“电风扇”</td>
</tr>
<tr>
<td>traits.intent</td>
<td>String</td>
<td>表示意图，详见1.3</td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th>语义标签</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td>action</td>
<td>操作的名称：打开，关闭，增加，降低等</td>
</tr>
<tr>
<td>attr</td>
<td>属性，比如客厅，卧室，餐厅等</td>
</tr>
<tr>
<td>device</td>
<td>标准化之后的设备名称，比如电视，空调，灯，热水器等</td>
</tr>
<tr>
<td>param</td>
<td>一些sub-commands，比如音量，温度等</td>
</tr>
<tr>
<td>value</td>
<td>sub-commands的取值</td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th>intent名字</th>
<th>意图说明</th>
</tr>
</thead>
<tbody>
<tr>
<td>other</td>
<td>表示控制指令</td>
</tr>
<tr>
<td>inquiry</td>
<td>表示查询指令</td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th>intent名字</th>
<th>意图说明</th>
<th>例句</th>
</tr>
</thead>
<tbody>
<tr>
<td>scene_dinner</td>
<td>就餐模式</td>
<td>开饭了</td>
</tr>
<tr>
<td>scene_meeting</td>
<td>会客模式</td>
<td>家里来客人了</td>
</tr>
<tr>
<td>scene_movie</td>
<td>影院模式</td>
<td>我要看电视</td>
</tr>
<tr>
<td>scene_open_all</td>
<td>全开模式</td>
<td>全部打开</td>
</tr>
<tr>
<td>scene_close_all</td>
<td>全关模式</td>
<td>全部关闭</td>
</tr>
</tbody>
</table>

