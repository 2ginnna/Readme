# 📖 Read Me
> **Verifiable Agent-to-Agent Social Protocol on Avalanche**

---

## 1. Project Definition

### 💡 One-Line Definition
**Read Me is an AI-agent based matching protocol where autonomous agents negotiate on behalf of users and settle the agreement on-chain with economic enforcement.**

### 🎯 What It Is
Read Me는 가벼운 탐색에 낭비되는 시간을 제거하고, AI 에이전트가 나를 대신해 관계의 깊이를 먼저 검증하는 **High-Fidelity Social Protocol**입니다. 우리는 찰나의 '스와이프'가 가진 불확실성을 거부합니다. 대신, 데이터로 증명되고 코드로 집행되는 **‘검증 가능한 합의(Verifiable Consensus)’**를 통해 가장 진실된 연결을 제안합니다.

> **"우리는 사람 간의 연결을 ‘스와이프’가 아니라 ‘검증 가능한 합의 과정(Verifiable Consensus)’으로 재정의합니다."**

---

### ⛓️ The Core Process

1. **Mirroring (Persona Creation)** 당신의 가치관, 취향, 대화의 결을 닮은 **Digital Twin**을 생성합니다. AI 에이전트는 당신과의 심도 있는 대화를 통해 '페르소나 상태'를 도출하고, 그 무결성(Model & Prompt version)을 Subnet에 해시로 각인합니다. 이것은 변조할 수 없는 당신의 디지털 지문입니다.

2. **Synthesis (Off-Chain Dialogue)** 당신의 에이전트와 상대의 에이전트가 오프체인 공간에서 밤새도록 협상을 수행합니다. 단순한 조건 검색이 아닙니다. 가치관의 정렬도(Alignment), 리스크 관리, 관계의 지속 가능성을 조율하며 두 사람의 '합의 가능성'을 도출합니다.

3. **Engraving (Consensus Anchoring)** 협상이 타결되는 순간, 대화의 정수(Transcript Root)와 최종 합의 조건이 Subnet에 앵커링됩니다. 양측 에이전트의 서명이 담긴 이 기록은 누구도 부정할 수 없는 **신뢰의 증거(Proof of Sincerity)**가 됩니다.

4. **Manifestation (On-Chain Settlement)** Avalanche Teleporter를 통해 합의 데이터가 C-Chain으로 전이됩니다. 관계의 시작을 상징하는 Relationship NFT가 발행됨과 동시에, 약속된 예치금(Stake)이 에스크로에 잠깁니다. 이후 대화 유지 조건(Check-in)에 따라 보상과 슬래싱이 코드로 자동 집행됩니다.

---

### ✨ Why It Matters

* **Proof of Sincerity:** 공허한 말 대신, 경제적 스테이킹으로 진심의 무게를 증명합니다.
* **Algorithmic Transparency:** AI의 판단 근거는 온체인 로그로 투명하게 추적 가능합니다.
* **Data Sovereignty:** 민감한 대화는 오프체인에 머물고, 검증된 결과값만이 온체인에서 자산화됩니다.

> **"Don't just Swipe. Re-read the Soul."** > 가벼운 연결은 비용이 되고, 진지한 몰입은 보상이 되는 새로운 소셜 프로토콜.

---

### What Makes It Different

| 구분 | Read Me (Consensus) | Legacy Apps (Swipe) |
| :--- | :--- | :--- |
| **Matching** | 페르소나를 닮은 에이전트 간 밀도 높은 협상의 결론 | 알고리즘에 의한 무작위 선택과 운 |
| **Sincerity** | 경제적 **Stake**를 통한 가치 증명 | 공허한 텍스트와 휘발되는 관심 |
| **Relationship** | 코드로 설계된 가장 견고한 **신뢰의 상태** | 감정의 파도에 휘둘리는 불안정한 연결 |

**Slogan: 가벼운 Swipe의 시대는 끝났습니다. 이제 Consensus로 연결될 시간.**


## 2. System Architecture

Read Me는 다음 구조를 채택합니다:

> 추론은 오프체인  
> 증명과 집행은 온체인

---

### Layer 1 — User & Private Layer (Off-Chain Intelligence)

**역할**

- 사용자 민감 데이터 처리  
- AI 추론 수행  
- Persona State 생성  

**기술**

- Vector DB (Pinecone / Milvus)  
- LLM (Local or API)  
- Client-side encryption  
- EIP-712 Typed Signature  

**동작 흐름**

1. 사용자는 AI 에이전트와 대화합니다.
2. AI는 Persona State를 생성합니다.
3. 다음과 같은 Commit을 생성합니다:

```text
persona_commit_hash = hash(
  persona_state ||
  model_id ||
  prompt_version ||
  timestamp ||
  salt
)
```

4. 사용자 지갑(또는 위임된 Agent Key)이 해당 Commit에 서명합니다.
5. Subnet에 Commit만 기록합니다.

**설계 원칙**

- 원본 데이터는 온체인에 기록되지 않습니다.
- 온체인은 데이터의 존재 및 무결성만 증명합니다.
- 추론은 완전히 오프체인에서 수행됩니다.

---

### Layer 2 — Negotiation Subnet (Custom Avalanche L1)

**역할**

- Agent 간 합의 앵커링
- 서명 검증
- Dispute 처리
- Stake 조건 정의

**중요 원칙**

협상 대화는 온체인에서 직접 수행되지 않습니다.

에이전트 간 협상은 오프체인에서 수행되며,  
Subnet은 합의 결과의 증명만 처리합니다.

---

### Negotiation Flow

1. Agent A와 Agent B가 오프체인에서 협상 수행
2. 협상 로그는 Merkle Tree 구조로 구성
3. 최종 합의 시 생성되는 데이터:

- `transcript_root`
- `agreement_terms_hash`
- `compatibility_score`
- `agentA_signature`
- `agentB_signature`

4. Subnet Smart Contract는 다음을 검증:

- 서명 유효성
- match_id 유일성
- Stake 조건 충족 여부

Subnet에는 전체 대화가 아닌  
**요약된 Root와 서명만 기록됩니다.**

---

### Gas Policy

Gas-less UX는 다음 구조로 구현됩니다:

- Relayer 기반 수수료 대납
- Rate limiting 적용
- Match 생성 시 Stake 요구

0 Gas는 무제한 무료를 의미하지 않습니다.  
스팸 방지를 위한 경제적 장치가 존재합니다.

---

## 3. Teleporter State Transition

합의 완료 후 흐름:

Negotiation L1  
→ Teleporter (ICM)  
→ Avalanche C-Chain  

Subnet에서 생성된 증명 데이터가  
C-Chain Settlement Contract로 전달됩니다.

**Compact Payload 구성**

- `match_id`
- `participants`
- `agreement_terms_hash`
- `transcript_root`
- `stake_amount`
- `expiration_time`

C-Chain에서는 다음이 실행됩니다:

- Relationship NFT 민팅
- Escrow 시작
- Slashing 조건 활성화

---

---

## 4. Relationship NFT & Trust-Flow

Relationship NFT는 단순한 소유형 자산이 아닙니다. 관계의 진정성을 데이터로 기록하고 강제하는 **'Dynamic Commitment Asset'**입니다.

### **📦 NFT Embedded Data**
* **Financial Layer:** Stake Amount (예치금 규모)
* **Time Layer:** Active Duration (관계 유지 기간), Check-in Requirement (체크인 빈도)
* **Rule Layer:** Slashing Rules (슬래싱 조건), Proof of Conversation (대화 무결성 증명)

### **🔄 Definitive Engagement: "Proof-of-Conversation"**
추상적인 '대화'를 기술적으로 정의하여 분쟁의 여지를 원천 차단합니다.
* **Mechanism:** 하루 1회 수행되는 온체인 **Check-in** 트랜잭션.
* **Success:** N일 연속 체크인 달성 시 예치금 반환 및 보상 지급.
* **Ghosting Re-defined:** 더 이상 감정의 영역이 아닙니다. **[Timeout + 미체크인]**이라는 명확한 코드로 정의되어 즉각적인 슬래싱을 집행합니다.

---

## 5. Economic Model: Trust-Fi

### **💰 1. Proof of Sincerity (Stake-to-Match)**
모든 매칭 요청에는 진지함을 증명하는 **경제적 기회비용**이 수반됩니다.
* **Success:** 조건 충족 시, 예치금(Stake) 반환 및 프로토콜 보상(Reward).
* **Failure:** 일방적 소통 단절 또는 조건 미달성 시, 예치금은 즉시 **Slashing** 처리됩니다.

### **🛠️ 2. Agent Upgrade Economy**
에이전트의 확장은 추상적 지표가 아닌 **'권한 및 정책의 확장'**으로 구현됩니다.
* **Multi-Thread NFT:** 동시 활성 협상 슬롯 확장.
* **Priority Access NFT:** 매칭 시도 횟수 및 알고리즘 우선순위권 부여.
* **Constraint Expansion:** 정확도와 같은 모호한 개념 대신 "데이터 접근 권한 및 정책 확장"으로 정의하여 온체인 검증 가능성을 유지합니다.

### **📈 3. Revenue Sources**
* **Primary Sales:** 기능 확장형 NFT 및 유틸리티 아이템 판매.
* **Secondary Royalty:** NFT 거래 발생 시 발생하는 수수료.
* **Slashing Pool:** 규칙 위반 시 발생하는 슬래싱 자산의 에코시스템 환원.

---

## 6. Why On-Chain?

* **Signature-based Consensus:** 모든 합의는 양측 에이전트의 디지털 서명으로만 증명됩니다.
* **Deterministic Enforcement:** 인간의 개입 없이 스마트 컨트랙트가 Stake 및 Slashing을 자동 집행합니다.
* **Data Anchoring:** Transcript Root를 통해 대화의 무결성을 사후 검증할 수 있는 투명성을 확보합니다.
* **Composability:** Relationship NFT는 다른 Avalanche 기반 앱과 연동되어 신뢰 지표로 활용될 수 있습니다.

---

## 7. Why Avalanche?

### **🚀 1. Custom L1 (Subnet)**
협상 앵커링과 로그 기록을 위한 전용 블록스페이스를 확보하여, 메인넷의 부하와 무관한 독립적 가스 정책을 운영합니다.

### **📡 2. Interchain Messaging (Teleporter)**
브릿지 없이 **[Subnet: 협상] ↔ [C-Chain: 자산화]**를 즉각 연결하여, 협상 결과가 즉시 자산으로 전이되는 심리스한 UX를 제공합니다.

### **⏱️ 3. Sub-second Finality**
1초 미만의 확정성을 통해 AI 에이전트 간의 실시간 합의와 NFT 민팅을 지연 없이 처리합니다.

---

## 8. MVP Scope
> **"Negotiation is Off-chain, Proof and Enforcement are On-chain."**

MVP는 프로토콜의 핵심 신뢰 레이어를 증명하는 다음 3가지 장면에 집중합니다:
1. **Persona Commit on L1:** 페르소나의 무결성을 Subnet에 박제.
2. **Agent Agreement Anchoring:** 에이전트 간 협상 로그 요약 및 온체인 서명.
3. **Teleport & NFT Manifestation:** Teleporter를 통한 상태 전이 및 C-Chain NFT 발행.

---

## 9. Vision

**Read Me는 단순한 서비스가 아닙니다.**

우리는 수백만 개의 AI 에이전트가 동시에 협상하고, 스스로 신뢰를 생성하며, 그 합의를 코드로 집행하는 **'Mass-Scale Consensus Infrastructure'**를 구축합니다.

**Swipe를 제거합니다. Consensus로 연결합니다.**

---
