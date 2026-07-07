# 톤 보존 발췌 요약: 기법의 근거와 출처

SKILL.md의 5단계 워크플로가 왜 그렇게 설계됐는지, 그리고 장르별로 무엇을 더 조심해야 하는지 정리한다. 웹 조사(2026-07-01)로 확인한 출처에 기반한다.

## 목차

1. 추출 우선이 톤을 살리는 이유
2. 5단계와 근거 매핑
3. 장르별 주의점
4. LLM이 톤을 평탄하게 만드는 메커니즘
5. 출처 목록

## 1. 추출 우선이 톤을 살리는 이유

요약에는 두 방식이 있다.

- 추출적(extractive): 원문 문장을 골라 이어 붙인다. 원문 문구·문체가 그대로 보존되어 충실하지만, 문장 사이 응집성이 약할 수 있다.
- 추상적(abstractive): 내용을 이해하고 새 문장으로 다시 쓴다. 유려하지만 톤·문체를 희생하고 환각 위험이 있다.

톤 보존 관점에서는 추출 비중을 높인 하이브리드가 정석이다. 원문 문장을 뼈대로 두고 경량 편집만 얹는 방식(TalkLess 논문류)이 화자의 말투를 보존하는 것으로 확인됐다. 다만 추출도 무비판적으로 신뢰하면 안 된다. 문장을 문맥에서 떼어내면 뜻이 바뀌어 오히려 불충실해질 수 있다("Extractive is not Faithful" 연구). 그래서 단계 5에서 충실성을 따로 점검한다.

## 2. 5단계와 근거 매핑

- 단계 1(구조 매핑): 구조를 먼저 고정하지 않으면 모델이 의미를 뭉개는 일반 요약으로 디폴트한다. 사람이 실체(substance)를 통제하고 AI는 효율만 돕는다는 원칙(ReadinGraphics FRAME 방법).
- 단계 2(추출): 품질은 더 나은 지시가 아니라 더 나은 원재료에서 나온다. 직접 고른 발췌문을 모델에 먹였을 때 결과가 결정적으로 덜 일반적이 됐다(Forte Labs 실험).
- 단계 3(외과적 압축): 원래 언어를 대부분 그대로 두고 외과적 절개만 한다("keeping most original language intact, making only surgical cuts", TalkLess).
- 단계 4(인용 보존): 잘 고른 인용(choice quotes)이 저자의 특별한 목소리를 반영한다(ReadinGraphics). 저자 문단 few-shot 주입은 추상적 "잘 요약해"보다 구체적 톤 차원(문장 길이·격식·직설성)을 명시할 때 효과가 크다.
- 단계 5(금지어 필터): "로봇 톤"을 고친 것은 모델 교체나 파인튜닝이 아니라 시스템 프롬프트와 명시적 금지 목록이었다.

## 3. 장르별 주의점

- 논픽션·논설·에세이: 이 스킬의 본령. 저자의 논지 전개와 핵심 주장 문장을 추출하면 잘 작동한다.
- 학술 논문: 초록이 이미 추상 요약이므로, 그것과 다른 가치를 주려면 저자의 논증 흐름·핵심 정의·결론 문장을 발췌하는 데 집중한다. 수식·표는 압축하지 말고 그대로 참조하게 둔다.
- 소설·서사: 가장 어렵다. Blinkist조차 픽션은 다루지 않는다. 페이싱·대화·문체 자체가 경험이라 압축하면 톤이 깨지기 때문이다. 픽션 요약 요청이 오면 이 한계를 사용자에게 먼저 알리고, 줄거리 요약이 아니라 "대표 문장 발췌 + 최소 연결" 쪽으로 합의한 뒤 진행한다.
- 기술 문서·매뉴얼: 톤보다 정확성이 우선인 장르다. 이 스킬보다 일반 요약이나 docparse 추출이 나을 수 있다. 저자 목소리 보존이 핵심 요구가 아니면 이 스킬을 쓰지 않아도 된다.

## 4. LLM이 톤을 평탄하게 만드는 메커니즘

LLM의 평탄한 기본 목소리는 RLHF가 정중하고 무난한 답을 보상해서 생긴 기본값이다. 연구들(P3SUM, "Voice Under Revision", "Catch Me If You Can")은 LLM이 개인 서사·문체를 체계적으로 평탄화(normalize)하며, 일상 저자의 암묵적 문체를 아직 잘 모방하지 못한다고 보고한다. 결론은 하나다. 톤 보존은 모델의 기본 능력이 아니라 워크플로로 강제해야 한다. 프롬프트 한 줄이 아니라 절차(추출 → 인용 보존 → 구조 고정 → 최소 윤문 → 금지어 필터)로 묶어야 안정적으로 보존된다.

## 5. 출처 목록

- TalkLess(추출 + 경량 편집으로 화자 말투 보존): https://arxiv.org/pdf/2507.15202
- 추출 vs 추상 요약 비교: https://www.deepknit.ai/blog/understanding-extractive-abstractive-summarization/
- Extractive is not Faithful(추출도 무비판 신뢰 금지): https://arxiv.org/pdf/2209.03549
- 책 요약에 AI 쓰는 법(인용·구조 보존, FRAME): https://readingraphics.com/guide-how-to-use-ai-to-summarize-a-book/
- ChatGPT로 책 요약하기(발췌 먹이기 실험): https://fortelabs.com/blog/how-to-summarize-books-using-chatgpt/
- LLM 기본 목소리와 시스템 프롬프트 교정: https://www.junia.ai/blog/llm-default-voice-ai-writing
- 톤 조정 프롬프트 예시: https://latitude.so/blog/10-examples-of-tone-adjusted-prompts-for-llms
- AI 글쓰기 패턴 제거·보이스 보정 프롬프트 모음: https://github.com/ai-boost/awesome-prompts
- Blinkist 제작 방식(인간 작가, 픽션 제외): https://www.blinkist.com/en/making_a_blink
- P3SUM(저자 관점 보존): https://arxiv.org/pdf/2311.09741
