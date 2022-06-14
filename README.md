<!-- PROJECT LOGO -->
<div align="center">
  <a href="https://github.com/osamhack2021/app_web_dronai_62bn">
    <img      
      src="https://user-images.githubusercontent.com/36218321/172825713-f95d8b00-ee94-4643-bee9-bb17bed99103.png"
      alt="Logo" width="256px" height="256px">
  </a>

  <h3 align="center">Unity Netcode</h3>

  <p align="center">
    유니티 넷코드에 대한 간략한 소개
    <br />
    <br />
    <a href="https://unity.com/" target="_blank">Unity3D</a>
    ·
    <a href="https://github.com/Unity-Technologies/com.unity.netcode.gameobjects" target="_blank">Netcode Repository</a>
    ·
    <a href="https://youtu.be/PCbJuSWBbrc" target="_blank">Video</a>
    ·
    <a href="https://github.com/LINEARJUN/SWTT-Unity-Netcode-Explanation/blob/main/NETCODE%20%EC%86%8C%EA%B0%9C%20PPT.pptx?raw=true" target="_blank">Presentation</a>
    <br />
    <br />
    <a href="https://github.com/LINEARJUN/SWTT-Unity-Netcode-Explanation/graphs/contributors">
      <img src="https://img.shields.io/github/contributors/LINEARJUN/SWTT-Unity-Netcode-Explanation.svg?style=for-the-badge" />
    </a>
    <a href="https://github.com/LINEARJUN/SWTT-Unity-Netcode-Explanation/network/members">
      <img src="https://img.shields.io/github/forks/LINEARJUN/SWTT-Unity-Netcode-Explanation.svg?style=for-the-badge" />
    </a>
    <a href="https://github.com/LINEARJUN/SWTT-Unity-Netcode-Explanation/stargazers">
      <img src="https://img.shields.io/github/stars/LINEARJUN/SWTT-Unity-Netcode-Explanation.svg?style=for-the-badge" />
    </a>
    <a href="https://github.com/LINEARJUN/SWTT-Unity-Netcode-Explanation/issues">
      <img src="https://img.shields.io/github/issues/LINEARJUN/SWTT-Unity-Netcode-Explanation.svg?style=for-the-badge" />
    </a>
    <a href="https://github.com/LINEARJUN/SWTT-Unity-Netcode-Explanation/blob/master/License.md">
      <img src="https://img.shields.io/github/license/LINEARJUN/SWTT-Unity-Netcode-Explanation.svg?style=for-the-badge" />
    </a>
  </p>
</div>

<h2>소개</h2>
<li>작성자 : 201920765 - 김준영</li>
<li>Unity Netcode에 대한 사진과 리소스는 <a href="https://unity.com">Unity</a>가 제작하였습니다.</li>
<li>현재 유뷰트에 올린 영상은 SWTT에 영상이 게시될 시 삭제됩니다!</li>

<h2> :books: 목차</h2>
<details open="open">
  <ol>
    <li><a href="#about"> 프로젝트 소개 (About)</a></li>
    <li><a href="#techniques"> 기능 설명 (Techniques)</a></li>
      <ul>
        <li><a href="#client"> Client RPC </a></li>
        <li><a href="#server"> Server RPC </a></li>
        <li><a href="#net_variables"> Network Variables </a></li>
        <li><a href="#rpc_net"> RPC vs Network Variables </a></li>
      </ul>
    <li><a href="#references"> 참조 (References)</a></li>
  </ol>
</details>

<h2 id="about">:exclamation: Unity Netcode 란 무엇인가?</h2>
<blockquote>유니티 엔진에서 사용되는 미드레벨 네트워킹 라이브러리이다. => <a href ="https://github.com/Unity-Technologies/com.unity.netcode.gameobjects">유니티 넷코드 공식 레포지토리</a></blockquote>
<img src="https://user-images.githubusercontent.com/36218321/173530541-6bd68132-1c17-4524-ab54-21f353e1b34c.jpg"></img>

<p>유니티 넷코드를 활용하면 비교적 네트워크 지식이 전문가들보다 떨어지더라도 네트워크 관련 기술을 라이브러리로 부터 가져와 쓸 수 있고 어려운 실시간 네트워크 통신 기술 구연들을 조금 더 쉽게 해볼 수 있다.</p>


<h2 id="techniques">:electric_plug: 기능 설명</h2>
<blockquote>넷코드에서 사용되는 대표적인 기능들 소개</blockquote>
<img src="https://user-images.githubusercontent.com/36218321/173532982-8dea78b4-2479-467a-b3d4-91a31100b853.png"></img>

<li>Netcode 버전 1.0.0 기준으로 설명 됨</li>
<li>일부 사진 자료 및 코드 자료는 Unity 측에서 제작함</li>
<li>더 많은 정보를 보고 싶다면 <a href="https://docs-multiplayer.unity3d.com/netcode/current/about">유니티 넷코드 공식 DOCS</a> 참고!</li>

<br/>

<!--라인 효과-->
<img src="https://user-images.githubusercontent.com/36218321/173535363-227603c9-3a2c-4d01-a2bc-d734ef1dba3d.gif"></a>

<h3 id="client">Client RPC</h3>
<blockquote>Can be invoked by the server to be executed on a client.</blockquote>
<img src="https://user-images.githubusercontent.com/36218321/173532561-cab28c97-d902-4b7e-ab21-724005f7e8e9.png"></img>

<p>서버가 자신에게 연결된 클라이언트들에게 원격 함수 호출을 해야할 때 사용하는 Attribute.</p>
<p>사용을 위해선 함수위에 반드시 [ClientRpc] Attribute가 붙어 있어야 하며 함수 이름은 ClientRpc로 끝나야 한다!</p>
<p>클라이언트 RPC는 일반적으로 서버에서만 호출될 수 있다!!</p>

```c#
[ClientRpc]
private void PongClientRpc(int somenumber, string sometext) { /* ... */ }
```

<hr/>

<h3 id="server">Server RPC</h3>
<blockquote>Can be invoked by a client to be executed on the server.</blockquote>
<img src="https://user-images.githubusercontent.com/36218321/173534716-e871944d-8762-4034-96c8-d686f658936c.png"></img>

<p>클라이언트가 서버에 있는 함수 호출을 요청 혹은 작업을 요청할 때 사용하는 Attribute.</p>
<p>사용을 위해선 함수위에 반드시 [ServerRpc] Attribute가 붙어 있어야 하며 함수 이름은 ServerRpc로 끝나야 한다!</p>
<p>서버 RPC는 일반적으로 클라이언트나 호스트에서만 호출될 수 있다!!</p>

```c#
[ServerRpc]
private void PingServerRpc(int somenumber, string sometext) { /* ... */ }
```

<hr/>

<h3 id="net_variables">Network Variables</h3>
<blockquote>다른 접속 클라이언트들과 주기적으로 동기화 되는 변수 형식</blockquote>

```c#
// everyone can read, only owner can write
public NetworkVariable<Vector3> NetPosition = new NetworkVariable<Vector3>(
    default,
    NetworkVariableBase.DefaultReadPerm, // Everyone
    NetworkVariableWritePermission.Owner
);
```

<p>주기적으로 다른 클라이언트들과 값을 계속 동기화해야 하는 변수가 있다면 위의 NetworkVariable<T> 를 사용하면 된다.</p>
<p>완전히 실시간으로 동기화 되는 것도 아니며 동기화 주기가 일정한 것도 아니다. 다만 계속 값을 교환할 뿐이다.</p>
<p>NetworkVariableBase. 에서 읽기 권한을 NetworkVariableWritePermission. 에서 쓰기 권한을 설정할 수 있다.</p>

<hr/>

<h3 id="rpc_net">RPC vs Network Variables</h3>
<blockquote>RPC 와 Network Variables 의 동작 차이</blockquote>

```c#
using Unity.Netcode;

public class TestNetworkScript : NetworkBehaviour
{
    /// <summary>
    /// This is network variable
    /// </summary>
    public NetworkVariable<bool> IsOpen { get; } = new NetworkVariable<bool>();
    
    // And RPCs
    [ServerRpc]
    private void TestServerRpc()
    {
      if(IsServer) TestClientRpc();
    }
    
    [ClientRpc]
    private void TestClientRpc()
    {
      // ~
    }
}

```

</br>

<blockquote>Network Variables 는 주기적으로 값을 동기화 하기 때문에 늦게 접속한 클라이언트들도 그 값을 받아 볼 수 있다!</blockquote>
<img src="https://user-images.githubusercontent.com/36218321/173540959-1112417f-811d-4760-ac14-577f7e58799b.png"></img>

<br/>

<blockquote>RPCs 는 호출하는 타이밍에서만 명령이 떨어지기에 늦게 접속하는 플레이어는 그 값이나 명령을 받아볼 수 없다!</blockquote>
<img src="https://user-images.githubusercontent.com/36218321/173541331-010362a7-0d93-4055-ab2c-205cacecf0f6.png"></img>

<p>즉 요약하자면 명령이나 값 전달을 원하는 시점에 호출 했을 때 Latency의 시간 이후 바로 클라이언트가 그 정보를 받아 보길 원한다면 RPCs를 사용하는 것이 좋다.</p>
<p>주기적으로 값을 동기화 해야 되고 늦게 접속한 플레이어도 값을 봐야 한다면 Network Variable을 사용하는 것이 더 적합하다.</p>


<h2 id="references">:mag: 참조 (References)</h2>
<blockquote>이번 발표를 진행하며 참조한 사이트</blockquote>


<li>유니티 공식 홈페이지 : <a href="https://unity.com">https://unity.com</a></li>
<li>유니티 공식 넷코드 Repository (MIT) : <a href="https://github.com/Unity-Technologies/com.unity.netcode.gameobjects">https://github.com/Unity-Technologies/com.unity.netcode.gameobjects</a></li>
<li>유니티 공식 넷코드 Documentation : <a href="https://docs-multiplayer.unity3d.com/netcode/current/about">https://docs-multiplayer.unity3d.com/netcode/current/about</a></li>
