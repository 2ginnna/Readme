# Read Me

### Verifiable Agent-to-Agent Social Protocol on Avalanche

---

## 1. Project Definition

**Read Me**는 단순한 소개팅 앱이 아닙니다.

이 프로젝트는 AI 에이전트가 인간을 대신해 협상하고,  
그 합의 결과를 **검증 가능한 형태로 온체인에 정산(Settlement)** 하는  
**Verifiable Agent-to-Agent Social Protocol**입니다.

데이트는 첫 번째 유스케이스일 뿐입니다.

이 프로토콜은 다음 영역으로 확장 가능합니다:

- Recruiting  
- Co-founder Matching  
- Business Partner Discovery  
- High-trust Social Coordination  

핵심은 다음입니다:

- AI가 나를 대신해 협상합니다.
- 합의 결과는 서명(Signature)과 증명(Proof)으로 온체인에 남습니다.
- 신뢰는 코드로 집행됩니다.

Swipe가 아니라 **Consensus**입니다.

---

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

## 4. Relationship NFT & Trust Enforcement

Relationship NFT는 단순한 정적 NFT가 아닙니다.

포함되는 요소:

- Stake amount
- Active duration
- Check-in requirement
- Slashing rule

---

### Proof of Conversation

“대화 유지”는 다음으로 정의됩니다:

- 하루 1회 On-Chain Check-in 트랜잭션
- N일 연속 체크인 시 조건 충족

이 구조는 다음을 보장합니다:

- 완전 자동 Slashing 가능
- 외부 오라클 의존 최소화
- 분쟁 없는 조건 집행

Ghosting은 감정이 아니라  
**Timeout + 미체크인**으로 정의됩니다.

---

## 5. Economic Model — Trust-Fi

### 1. Proof of Sincerity

매칭 요청 시 Stake 예치

**성공**
- 조건 충족 → Stake 반환 + Reward

**실패**
- Timeout → Slashing

진지함은 경제적 비용으로 증명됩니다.

---

### 2. Agent Upgrade Economy (NFT 기반)

Agent 기능 확장은 NFT 권한 모델로 구현됩니다.

예시:

- Multi-Thread NFT  
  → 동시 활성 협상 슬롯 증가

- Priority Access NFT  
  → 추가 매칭 시도 가능

정확도 상승과 같은 추상 개념은  
온체인 검증이 불가능하므로  
“권한 및 정책 확장”으로 정의됩니다.

---

### 3. Revenue Sources

- NFT Primary Sales  
- Secondary Royalty  
- Slashing Pool  
- Premium Matching Features  

---

## 6. Why On-Chain

1. Signature-based Consensus  
   합의는 양측 서명으로 증명됩니다.

2. Deterministic Enforcement  
   Stake 및 Slashing은 자동 집행됩니다.

3. Data Anchoring  
   Transcript Root를 통한 사후 검증 가능성 확보

4. Composability  
   Relationship NFT는 다른 Avalanche 기반 앱과 연동 가능합니다.

---

## 7. Why Avalanche

### 1. Custom L1 (Subnet)

- App-specific blockspace 확보
- 협상 앵커링 전용 체인 구성
- 독립적 정책 설정 가능

### 2. Interchain Messaging (Teleporter)

- 브릿지 없이 상태 전이
- 협상 → 자산화 즉시 연결

### 3. Sub-second Finality

- 실시간 UX 구현 가능

---

## 8. MVP Scope

MVP는 다음 3가지에 집중합니다:

1. Persona Commit on L1  
2. Agent Agreement Anchoring  
3. Teleport & Relationship NFT Mint  

협상은 오프체인  
증명과 집행은 온체인

---

## 9. Vision

Read Me는 앱이 아닙니다.

수백만 개의 AI 에이전트가  
동시에 협상하고  
합의를 생성하며  
신뢰를 코드로 집행하는  

Mass-Scale Consensus Network를 구축합니다.

Swipe를 제거합니다.  
Consensus로 연결합니다.
