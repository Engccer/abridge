# abridge

원문의 톤 앤 매너(저자의 목소리·문체·리듬)를 보존하면서 분량만 줄이는 발췌형(abridged, Blinkist 스타일) 요약 스킬이다. 재서술하지 않고 발췌한다. LLM이 요약할 때 흔히 나타나는 평탄한 설명체·불릿 나열·매끈한 재서술을 피하고, 저자가 실제로 쓴 문장을 뼈대로 삼는다.

## 워크플로

구조 매핑(저자의 골격을 먼저 고정) → 추출(핵심 원문 문장을 그대로 골라냄) → 외과적 압축(문장 자체는 유지하고 군더더기만 잘라냄) → 목소리·인용 보존(특징적 표현과 직접 인용 유지) → 금지어 필터(AI 상투어·em dash 등 제거 후 분량·구조·충실성 점검)의 5단계로 진행한다. 각 단계가 톤 보존 장치이며, 단계를 건너뛰면 평탄한 요약으로 디폴트한다. 기본 압축률은 원문 대비 15~25%다.

## 선택 후처리 (요청 시에만)

요약이 끝난 뒤 사용자가 요청하면 윤문 → 번역 → 오디오북 순으로 얹을 수 있다. 명시적 요청이 없으면 요약·번역·오디오북 모두 원문 언어를 따른다. 번역은 목표 언어 미지정 시 한국어로, 재요약 없이 1:1로 옮긴다. 오디오북 생성은 이 저장소에 동봉된 ElevenLabs TTS 스크립트(`scripts/elevenlabs_tts.py`)로 수행하므로 별도 스킬 설치가 필요 없다(Python + `elevenlabs` 패키지 + `ELEVENLABS_API_KEY` 필요, 유료 API 비용 발생. 원본: [speech-toolkit](https://github.com/Engccer/speech-toolkit)).

## 설치

```bash
npx skills add Engccer/abridge -g
```

이 저장소는 [skills-for-the-blind](https://github.com/Engccer/skills-for-the-blind) 번들의 일부다. 접근성을 고려해 만든 Claude Code 스킬 모음이며, 각 스킬은 독립적으로도 설치해 쓸 수 있다.

## License

MIT (c) 2026 Engccer

---

## English

abridge is a Claude Code skill for creating tone-preserving, extractive (abridged, Blinkist-style) summaries of documents, articles, and books. Instead of paraphrasing, it extracts and lightly trims the author's own sentences, avoiding the generic flat, bullet-heavy LLM summary style.

**Workflow:** structure mapping (lock the author's outline first) → extraction (pull key sentences verbatim) → surgical cuts (trim filler, keep sentence form) → voice and quote preservation (keep distinctive phrasing, quote 1-3 memorable lines directly) → forbidden-phrase filter (strip AI cliches and em dashes, then check length/structure/faithfulness). Default target length is 15-25% of the original.

**Optional post-processing (only when explicitly requested):** tone polishing, translation (defaults to Korean if no target language is given, 1:1 faithful, no re-summarizing), and audiobook narration via the bundled ElevenLabs TTS script (`scripts/elevenlabs_tts.py`; no extra skill install needed; requires Python, the `elevenlabs` package, and a paid `ELEVENLABS_API_KEY`; upstream source: [speech-toolkit](https://github.com/Engccer/speech-toolkit)).

**Install:**

```bash
npx skills add Engccer/abridge -g
```

Part of the [skills-for-the-blind](https://github.com/Engccer/skills-for-the-blind) bundle of accessibility-minded Claude Code skills. Each skill also works standalone.

**License:** MIT (c) 2026 Engccer
