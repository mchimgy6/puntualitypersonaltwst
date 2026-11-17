[ai_studio_code.html](https://github.com/user-attachments/files/34962594/ai_studio_code.html)[<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>결 (GYEOL) — MBTI × 정치 성향 16문항 설문</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@600&family=IBM+Plex+Mono:wght@400;500&family=Noto+Sans+KR:wght@400;500;600;700&family=Noto+Serif+KR:wght@500;600;700&display=swap"
      rel="stylesheet"
    />
    <style>
      :root {
        --bg: #f7f4ee;
        --card: #fbf9f5;
        --stone: #ebe6df;
        --ink: #1c1917;
        --sub: #44403c;
        --muted: #78716c;
        --border: #e7e5e4;
        --border-strong: #d6d3d1;
        --accent: #1b4332;
        --slate: #2b3a55;
        --serif: 'Cormorant Garamond', 'Noto Serif KR', Georgia, serif;
        --sans: 'Noto Sans KR', -apple-system, BlinkMacSystemFont, sans-serif;
        --mono: 'IBM Plex Mono', ui-monospace, monospace;
      }
      *, *::before, *::after { box-sizing: border-box; }
      body {
        margin: 0;
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        background: var(--bg);
        color: var(--ink);
        font-family: var(--sans);
        line-height: 1.65;
        -webkit-font-smoothing: antialiased;
      }
      button { font-family: inherit; cursor: pointer; border: none; background: none; color: inherit; }
      button:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; }
      .serif { font-family: var(--serif); }
      .mono { font-family: var(--mono); font-variant-numeric: tabular-nums; }
      .wrap { width: 100%; max-width: 980px; margin: 0 auto; padding: 0 20px; }
      .wrap-narrow { width: 100%; max-width: 760px; margin: 0 auto; padding: 0 20px; }

      header {
        border-bottom: 1px solid var(--border);
        background: rgba(247, 244, 238, 0.95);
      }
      .header-in {
        max-width: 980px;
        margin: 0 auto;
        padding: 14px 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 16px;
      }
      .brand { font-family: var(--serif); font-size: 20px; font-weight: 600; white-space: nowrap; }
      .nav { display: flex; align-items: center; gap: 20px; font-size: 13px; color: var(--muted); }
      .nav button:hover { color: var(--ink); text-decoration: underline; text-underline-offset: 4px; }

      .btn-primary {
        display: inline-flex; align-items: center; justify-content: center; gap: 8px;
        min-height: 42px; padding: 9px 18px; border-radius: 6px;
        background: var(--accent); color: var(--bg); font-size: 13px; font-weight: 500; white-space: nowrap;
      }
      .btn-primary:hover { background: #143326; }
      .btn-outline {
        display: inline-flex; align-items: center; justify-content: center; gap: 8px;
        min-height: 42px; padding: 9px 16px; border-radius: 6px;
        border: 1px solid var(--border-strong); color: var(--ink); font-size: 13px; font-weight: 500; white-space: nowrap;
      }
      .btn-outline:hover { background: rgba(235, 230, 223, 0.55); border-color: var(--muted); }

      main { flex: 1; padding: 40px 0 64px; }
      .section { border-bottom: 1px solid var(--border); padding: 40px 0; }
      .section:last-child { border-bottom: none; }
      .kicker { margin: 0; font-size: 12px; color: var(--muted); }
      h1 { font-family: var(--serif); font-size: clamp(1.9rem, 3.6vw, 2.75rem); line-height: 1.25; margin: 12px 0 0; }
      h2 { font-family: var(--serif); font-size: clamp(1.4rem, 2.4vw, 1.75rem); line-height: 1.3; margin: 8px 0 0; }

      .grid-2 { display: grid; gap: 20px; margin-top: 24px; }
      .grid-4 { display: grid; gap: 12px; margin-top: 14px; }
      @media (min-width: 680px) {
        .grid-2 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
        .grid-4 { grid-template-columns: repeat(4, minmax(0, 1fr)); }
      }

      .card { border: 1px solid var(--border); border-radius: 8px; background: var(--card); padding: 22px; }
      .sub-card { border: 1px solid var(--border); border-radius: 6px; background: var(--bg); padding: 14px; }

      /* Quiz */
      .progress-bg { height: 3px; width: 100%; background: var(--border); border-radius: 999px; overflow: hidden; margin-top: 14px; }
      .progress-fill { height: 100%; background: var(--accent); transform-origin: left; transition: transform 0.2s ease; }
      .steps { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 12px; }
      .step {
        width: 28px; height: 24px; border-radius: 4px; font-family: var(--mono); font-size: 11px;
        background: rgba(231, 229, 228, 0.45); color: #a8a29e;
      }
      .step.done { background: var(--stone); color: var(--ink); }
      .step.active { background: var(--ink); color: var(--bg); }
      .step:disabled { cursor: not-allowed; }

      .choice {
        display: flex; flex-direction: column; justify-content: space-between;
        min-height: 68px; padding: 12px 14px; border-radius: 8px; text-align: left;
        border: 1px solid var(--border-strong); background: var(--card); transition: all 0.15s ease;
      }
      .choice:hover { border-color: var(--muted); background: rgba(235, 230, 223, 0.6); }
      .choice.selected { border-color: var(--accent); background: var(--accent); color: var(--bg); }

      /* Spectrum Bars */
      .spectrum-track { position: relative; height: 10px; border-radius: 999px; background: var(--border); margin-top: 8px; }
      .spectrum-dot {
        position: absolute; top: 50%; width: 16px; height: 16px; border-radius: 999px;
        background: var(--accent); border: 2px solid var(--bg); transform: translate(-50%, -50%);
      }
      .dual-bar { display: flex; height: 10px; border-radius: 999px; overflow: hidden; background: var(--border); margin-top: 10px; }

      footer { border-top: 1px solid var(--border); padding: 28px 0; font-size: 12px; color: var(--muted); }
    </style>
  </head>
  <body>
    <header>
      <div class="header-in">
        <button type="button" class="brand" data-act="home">결 GYEOL · 정치 성향</button>
        <div class="nav">
          <button type="button" data-act="home" data-sec="axes">핵심 지표 상관관계</button>
          <button type="button" data-act="start" id="header-start">16문항 설문 시작</button>
        </div>
      </div>
    </header>

    <main id="app"></main>

    <footer>
      <div class="wrap" style="display:flex;flex-wrap:wrap;justify-content:space-between;gap:12px;">
        <span>심리학·정치학 연구(빅5 성격 모델 및 MBTI 연계 연구) 기반 16문항 설문</span>
        <span>성격은 정치 태도를 완전히 결정하지 않으며 약한 상관관계의 참고 지표입니다.</span>
      </div>
    </footer>

    <script>
      (function () {
        const AXES = [
          {
            key: 'SN',
            title: '감각(S) vs 직관(N) — 가장 뚜렷한 차이',
            sub: '문항 01–04 · 변화와 안정에 대한 인식',
            left: { letter: 'S', name: '감각 (Sensing)', desc: '현실적 경험, 검증된 사실, 실용성과 안정을 중시해 기존 제도와 전통을 유지하려는 보수적 가치와 잘 맞습니다.' },
            right: { letter: 'N', name: '직관 (iNtuition)', desc: '추상적 개념, 미래 가능성, 체제 변화와 새로운 시도에 개방적이어서 개혁적·진보적 가치를 선호하는 비율이 높습니다.' },
          },
          {
            key: 'TF',
            title: '사고(T) vs 감정(F) — 정책 우선순위의 차이',
            sub: '문항 05–08 · 효율·규칙과 공감·복지 기준',
            left: { letter: 'T', name: '사고 (Thinking)', desc: '객관적 효율성, 공정한 규칙, 개인의 책임과 성취 보상을 중시해 시장주의나 능력주의 관점(경제 보수)을 지지하는 편입니다.' },
            right: { letter: 'F', name: '감정 (Feeling)', desc: '타인의 고통에 대한 공감, 사회적 약자 보호, 공동체 조화를 중시해 분배와 복지 정책(사회 진보)에 우호적인 편입니다.' },
          },
          {
            key: 'JP',
            title: '판단(J) vs 인식(P) — 질서와 자율에 대한 태도',
            sub: '문항 09–12 · 법치·규범과 유연성·자유',
            left: { letter: 'J', name: '판단 (Judging)', desc: '명확한 규칙, 체계, 질서, 예측 가능성을 선호하므로 법치와 사회적 규범을 강조하는 보수적 태도와 연결됩니다.' },
            right: { letter: 'P', name: '인식 (Perceiving)', desc: '유연성, 자율성, 권위에 대한 의구심이 강해 기존 규범의 해체나 개인의 자유 확장을 중시하는 진보·자유주의 경향이 있습니다.' },
          },
          {
            key: 'EI',
            title: '외향(E) vs 내향(I) — 정치 참여 방식의 차이',
            sub: '문항 13–16 · 이념 방향과는 거의 무관',
            left: { letter: 'I', name: '내향 (Introversion)', desc: '진보·보수 이념 자체와는 상관이 거의 없으며, 자료 숙고와 온라인 의견 개진, 조용한 투표 방식의 참여로 나타납니다.' },
            right: { letter: 'E', name: '외향 (Extraversion)', desc: '진보·보수 이념 자체와는 상관이 거의 없으며, 집회·오프라인 토론·모임 등 적극적 행동 중심의 참여로 나타납니다.' },
          },
        ];

        const QUESTIONS = [
          // S vs N (문항 1-4)
          {
            id: 1, axis: 'SN', label: 'S / N · 가장 뚜렷한 차이 (변화와 안정)', scene: '사회 제도의 개선 방향',
            prompt: '현재 사회 제도에 한계가 보일 때, 우리가 택해야 할 변화의 속도와 방식은 어느 쪽에 더 가깝나요?',
            poleA: 'S', textA: '검증된 현행 제도와 안정을 지키면서, 실제 경험으로 확인된 문제만 단계적으로 보완해 가는 편이 낫다.',
            poleB: 'N', textB: '기존 틀의 한계가 분명하다면, 미래의 가능성을 열어두는 새로운 구조와 체제 변화를 과감히 시도해야 한다.',
            anchor: true,
          },
          {
            id: 2, axis: 'SN', label: 'S / N · 가장 뚜렷한 차이 (변화와 안정)', scene: '정책 공약을 판단하는 기준',
            prompt: '새로운 정책 제안을 접했을 때, 내가 더 신뢰하고 마음이 움직이는 설득 포인트는 무엇인가요?',
            poleA: 'S', textA: '당장 실행 가능한 현실적 예산, 검증된 과거 사례, 구체적이고 실용적인 수치 근거.',
            poleB: 'N', textB: '이 정책이 앞으로 사회의 큰 방향과 미래 세대의 가능성을 어떻게 바꾸어 놓을지에 대한 비전.',
          },
          {
            id: 3, axis: 'SN', label: 'S / N · 가장 뚜렷한 차이 (변화와 안정)', scene: '전통과 관습에 대한 시선',
            prompt: '오랫동안 사회를 지탱해 온 전통이나 익숙한 관습을 마주했을 때, 나의 자연스러운 태도는 어느 쪽인가요?',
            poleA: 'S', textA: '오랜 시간을 견딘 관습에는 검증된 지혜와 사회 안정을 지탱하는 실용적 가치가 담겨 있다.',
            poleB: 'N', textB: '과거의 기준이 현재와 맞지 않는다면, 더 나은 대안을 상상하며 과감히 재구성해 나가야 한다.',
          },
          {
            id: 4, axis: 'SN', label: 'S / N · 가장 뚜렷한 차이 (변화와 안정)', scene: '위기 상황의 해법 선택',
            prompt: '예상치 못한 사회·경제적 위기가 닥쳤을 때, 먼저 고려해야 한다고 느끼는 대응 방향은 무엇인가요?',
            poleA: 'S', textA: '이미 효과가 검증된 기존 매뉴얼과 안정적 수단을 우선 적용해 부작용과 혼란을 최소화한다.',
            poleB: 'N', textB: '기존 방식이 통하지 않는 새로운 국면일 수 있으므로, 발상을 전환한 개혁적·실험적 해법을 모색한다.',
          },

          // T vs F (문항 5-8)
          {
            id: 5, axis: 'TF', label: 'T / F · 정책 우선순위 (효율 vs 복지)', scene: '경제 성장과 복지 분배',
            prompt: '한정된 국가 재원을 배분할 때, 장기적으로 더 우선순위를 두어야 한다고 느끼는 방향은 어느 쪽인가요?',
            poleA: 'T', textA: '객관적 효율성과 시장 활력을 높이고, 개인의 책임과 성취에 비례해 보상이 돌아가는 구조.',
            poleB: 'F', textB: '타인의 어려움을 헤아려 사회적 약자를 보호하고, 공동체 전체가 함께 살아가는 복지·분배 안전망.',
            anchor: true,
          },
          {
            id: 6, axis: 'TF', label: 'T / F · 정책 우선순위 (효율 vs 복지)', scene: '공정함의 기준',
            prompt: '사회적 논쟁에서 "공정하다"는 말을 들었을 때, 가장 먼저 떠올리는 기준은 무엇인가요?',
            poleA: 'T', textA: '모두에게 동일한 규칙이 예외 없이 적용되고, 노력과 역량의 결과에 따라 합리적으로 평가받는 원칙.',
            poleB: 'F', textA: '출발선이 다른 이들의 고통과 처지를 먼저 살피고, 누구도 공동체에서 소외되지 않도록 보듬는 조화.',
          },
          {
            id: 7, axis: 'TF', label: 'T / F · 정책 우선순위 (효율 vs 복지)', scene: '공공 사업 평가 잣대',
            prompt: '정부나 지자체의 공공 정책을 평가할 때, 내가 더 중요하게 따져보는 지점은 무엇인가요?',
            poleA: 'T', textA: '투입 비용 대비 객관적 성과, 재정 효율성, 규칙이 일관되게 작동하는지 여부.',
            poleB: 'F', textA: '수치로 다 잡히지 않더라도 취약 계층의 고통을 얼마나 덜어주었는지, 공동체 온기를 지켰는지 여부.',
          },
          {
            id: 8, axis: 'TF', label: 'T / F · 정책 우선순위 (효율 vs 복지)', scene: '사회적 갈등 조정',
            prompt: '서로 다른 계층이나 집단의 이해가 충돌할 때, 문제를 푸는 데 먼저 필요한 태도는 무엇이라고 보시나요?',
            poleA: 'T', textA: '감정적 호소보다 객관적 사실과 법적·논리적 타당성을 따져 명확한 기준선을 세우는 일.',
            poleB: 'F', textA: '당사자들이 겪는 상처와 입장의 맥락에 충분히 공감해 주어 실질적인 화해의 기반을 닦는 일.',
          },

          // J vs P (문항 9-12)
          {
            id: 9, axis: 'JP', label: 'J / P · 질서와 자율 (규범 vs 자유)', scene: '법치와 개인의 자유',
            prompt: '사회의 질서와 개인의 자유로운 선택이 긴장 관계에 놓일 때, 내가 더 중시하는 쪽은 무엇인가요?',
            poleA: 'J', textA: '명확한 법치와 사회적 규범이 지켜져야 예측 가능한 공동체 질서가 유지된다.',
            poleB: 'P', textB: '기존 규범이나 권위가 개인의 자율성과 다양한 선택권을 지나치게 억압하지 않는지 의심해 보아야 한다.',
            anchor: true,
          },
          {
            id: 10, axis: 'JP', label: 'J / P · 질서와 자율 (규범 vs 자유)', scene: '제도 운영의 유연성',
            prompt: '공적 제도와 규칙을 운영할 때, 사회를 더 건강하게 만든다고 느끼는 방식은 어느 쪽인가요?',
            poleA: 'J', textA: '명확한 체계와 단계별 원칙을 세워 일관성 있게 집행해야 사회적 혼선을 줄일 수 있다.',
            poleB: 'P', textB: '변화하는 상황에 맞추어 규칙을 유연하게 열어두고, 현장의 자율적 판단 여지를 넓혀두어야 한다.',
          },
          {
            id: 11, axis: 'JP', label: 'J / P · 질서와 자율 (규범 vs 자유)', scene: '권위와 규범에 대한 태도',
            prompt: '오래 통용되어 온 공적 권위나 사회적 관행을 대할 때, 나의 자연스러운 시선은 어떤가요?',
            poleA: 'J', textA: '공동체의 안정을 위해 정당한 절차로 세워진 권위와 규범은 우선 존중하고 따르는 편이 합당하다.',
            poleB: 'P', textB: '권위나 관행이라는 이유만으로 받아들이기보다, 타당한지 질문하고 자유로운 대안을 모색하는 편이다.',
          },
          {
            id: 12, axis: 'JP', label: 'J / P · 질서와 자율 (규범 vs 자유)', scene: '공적 합의의 마무리',
            prompt: '사회적 의제에 대한 논의가 길어질 때, 어떤 방향으로 정리되길 바라는 편인가요?',
            poleA: 'J', textA: '정해진 기한과 절차 안에서 분명한 결론을 내려 불확실성을 해소하는 편이 낫다.',
            poleB: 'P', textB: '시간이 더 걸리더라도 다양한 소수 의견과 개인의 자유를 닫지 않고 열린 상태로 논의를 이어가는 편이 낫다.',
          },

          // E vs I (문항 13-16)
          {
            id: 13, axis: 'EI', label: 'E / I · 정치 참여 방식 (행동 vs 숙고)', scene: '목소리를 내는 방식',
            prompt: '관심 있는 정치·사회 이슈가 생겼을 때, 내가 가장 편안하게 느끼는 참여 방식은 무엇인가요?',
            poleA: 'I', textA: '관련 자료를 혼자 읽고 생각을 정리한 뒤, 온라인으로 의견을 남기거나 조용히 투표로 표현한다.',
            poleB: 'E', textB: '사람들과 직접 만나 토론하거나 집회·공청회·모임 등 현장에 직접 참여하며 의견을 나눈다.',
            anchor: true,
          },
          {
            id: 14, axis: 'EI', label: 'E / I · 정치 참여 방식 (행동 vs 숙고)', scene: '입장을 정리하는 과정',
            prompt: '특정 정책이나 후보에 대한 나의 생각이 가장 선명하게 다듬어지는 순간은 언제인가요?',
            poleA: 'I', textA: '방해받지 않는 조용한 시간에 자료와 공약을 혼자 차분히 비교·분석할 때.',
            poleB: 'E', textB: '여러 사람과 활발하게 대화를 주고받고 공개적인 토론을 거치면서 생각을 발전시킬 때.',
          },
          {
            id: 15, axis: 'EI', label: 'E / I · 정치 참여 방식 (행동 vs 숙고)', scene: '선거 및 공적 캠페인 기간',
            prompt: '선거철이나 사회적 캠페인이 활발한 시기, 나의 실제 행동과 가장 가까운 모습은 무엇인가요?',
            poleA: 'I', textA: '주변에 드러내기보다 내 기준대로 공약을 살핀 뒤 조용히 투표소에 다녀오는 편이다.',
            poleB: 'E', textB: '지인들과 적극적으로 쟁점을 이야기하고, 뜻을 같이하는 사람들과 현장 활동을 함께하는 편이다.',
          },
          {
            id: 16, axis: 'EI', label: 'E / I · 정치 참여 방식 (행동 vs 숙고)', scene: '정치 대화 후 에너지 변화',
            prompt: '여럿이 모여 사회 이슈나 정치 이야기를 한 시간 넘게 나눈 뒤 돌아왔을 때의 기분은 어떠한가요?',
            poleA: 'I', textA: '흥미로운 이야기였더라도 에너지가 소모되어 당분간은 혼자 조용히 쉬며 생각을 가라앉히고 싶다.',
            poleB: 'E', textB: '생각을 나누며 오히려 활력이 돌고, 다른 사람들과도 계속 이야기를 이어가고 싶어진다.',
          },
        ];

        const TYPE_TITLES = {
          INTJ: '구조 개혁(N) · 합리적 효율(T) · 체계 질서(J) · 숙고형 참여(I)',
          INTP: '대안 탐색(N) · 논리 원칙(T) · 개인 자율(P) · 숙고형 참여(I)',
          ENTJ: '거시 비전(N) · 성과 효율(T) · 명확한 질서(J) · 적극 참여(E)',
          ENTP: '체제 혁신(N) · 논리 토론(T) · 규범 유연성(P) · 적극 참여(E)',
          INFJ: '미래 대안(N) · 복지 공감(F) · 원칙 질서(J) · 숙고형 참여(I)',
          INFP: '이상적 대안(N) · 약자 공감(F) · 개인 자유(P) · 숙고형 참여(I)',
          ENFJ: '공동체 비전(N) · 복지 조화(F) · 책임 규범(J) · 적극 참여(E)',
          ENFP: '새로운 가능성(N) · 공감 연대(F) · 자유 다양성(P) · 적극 참여(E)',
          ISTJ: '검증된 안정(S) · 공정 원칙(T) · 법치 질서(J) · 숙고형 참여(I)',
          ISFJ: '생활 안정(S) · 돌봄 공감(F) · 규범 존중(J) · 숙고형 참여(I)',
          ESTJ: '현실 실용(S) · 시장 책임(T) · 법치 질서(J) · 적극 참여(E)',
          ESFJ: '공동체 안정(S) · 배려 조화(F) · 규범 존중(J) · 적극 참여(E)',
          ISTP: '현실 실용(S) · 합리 효율(T) · 개인 자율(P) · 숙고형 참여(I)',
          ISFP: '생활 체감(S) · 약자 공감(F) · 일상 자율(P) · 숙고형 참여(I)',
          ESTP: '현장 실용(S) · 성과 효율(T) · 유연한 자율(P) · 적극 참여(E)',
          ESFP: '체감 현실(S) · 사람 공감(F) · 열린 유연성(P) · 적극 참여(E)',
        };

        const CHOICES = [
          { val: -2, key: '1', label: '확실히 A', sub: '내 태도와 매우 가깝다' },
          { val: -1, key: '2', label: '대체로 A', sub: 'A 쪽에 더 기운다' },
          { val: 1, key: '3', label: '대체로 B', sub: 'B 쪽에 더 기운다' },
          { val: 2, key: '4', label: '확실히 B', sub: '내 태도와 매우 가깝다' },
        ];

        const state = { view: 'home', idx: 0, answers: {}, result: null, copied: false };

        function esc(s) {
          return String(s).replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
        }

        function computeResult() {
          const axes = AXES.map((a) => {
            const qs = QUESTIONS.filter((q) => q.axis === a.key);
            let lRaw = 0, rRaw = 0, anchorPole = a.left.letter;
            qs.forEach((q) => {
              const v = state.answers[q.id];
              if (!v) return;
              const pole = v < 0 ? q.poleA : q.poleB;
              if (pole === a.left.letter) lRaw += Math.abs(v);
              else rRaw += Math.abs(v);
              if (q.anchor) anchorPole = pole;
            });
            let lPct = 50, rPct = 50, winner = anchorPole, close = false;
            if (lRaw + rRaw > 0) {
              if (lRaw === rRaw) {
                close = true;
                lPct = winner === a.left.letter ? 52 : 48;
                rPct = 100 - lPct;
              } else {
                lPct = Math.round((lRaw / (lRaw + rRaw)) * 100);
                rPct = 100 - lPct;
                winner = lRaw > rRaw ? a.left.letter : a.right.letter;
                close = Math.abs(lPct - rPct) <= 12;
              }
            }
            return {
              key: a.key, title: a.title,
              lPole: a.left.letter, lName: a.left.name.split(' ')[0], lPct,
              rPole: a.right.letter, rName: a.right.name.split(' ')[0], rPct,
              winner, winnerPct: winner === a.left.letter ? lPct : rPct, close,
            };
          });

          const get = (k) => axes.find((x) => x.key === k);
          const typeCode = ['EI', 'SN', 'TF', 'JP'].map((k) => get(k).winner).join('');
          // S/N(45%), T/F(30%), J/P(25%) 기반 진보-보수 가치 스펙트럼 산출 (0=S·T·J 보수 경향, 100=N·F·P 진보 경향)
          const spectrum = Math.round(get('SN').rPct * 0.45 + get('TF').rPct * 0.30 + get('JP').rPct * 0.25);

          let spectrumLabel = '균형적 중도 스펙트럼 (S·T·J와 N·F·P 혼재)';
          let spectrumDesc = '안정·효율·질서 지표(S·T·J)와 변화·공감·자율 지표(N·F·P)가 고르게 나타났습니다. 사안별로 실용적 안정과 구조적 변화를 유연하게 오가는 편입니다.';
          if (spectrum >= 65) {
            spectrumLabel = '변화·공감·자율 지향 (진보 성향과 닿아 있는 결)';
            spectrumDesc = '직관(N)·감정(F)·인식(P) 비중이 높습니다. 체제 변화와 새로운 대안에 열려 있고(N), 약자 보호와 복지(F), 개인의 자율성(P)을 중시하는 진보적 가치와 상관관계가 나타나는 편입니다.';
          } else if (spectrum >= 54) {
            spectrumLabel = '온건 개혁·균형 지향 (중도 진보 측 스펙트럼)';
            spectrumDesc = '변화와 공감, 자율성에 다소 무게를 두면서도 현실적 기준을 함께 살피는 편입니다.';
          } else if (spectrum <= 35) {
            spectrumLabel = '안정·원칙·질서 지향 (보수 성향과 닿아 있는 결)';
            spectrumDesc = '감각(S)·사고(T)·판단(J) 비중이 높습니다. 검증된 제도와 안정(S), 효율과 공정한 규칙(T), 법치와 사회적 규범(J)을 중시하는 보수적 가치와 상관관계가 나타나는 편입니다.';
          } else if (spectrum <= 46) {
            spectrumLabel = '온건 안정·원칙 지향 (중도 보수 측 스펙트럼)';
            spectrumDesc = '현실 검증과 효율, 규범의 기준에 다소 무게를 두며 점진적 보완을 선호하는 편입니다.';
          }

          const ePct = get('EI').rPct;
          let partLabel = '균형형 참여 (상황에 따라 전환)';
          let partDesc = '이념 방향과 무관하게, 혼자 자료를 숙고해 투표하거나(I) 필요한 자리에서 직접 대화·현장에 참여하는(E) 방식을 병행합니다.';
          if (ePct >= 58) {
            partLabel = '적극 행동형 참여 (외향 E 중심)';
            partDesc = '진보·보수 이념과 무관하게, 집회·토론·모임 등 직접 목소리를 내는 행동 중심의 참여를 선호합니다.';
          } else if (ePct <= 42) {
            partLabel = '차분한 숙고형 참여 (내향 I 중심)';
            partDesc = '진보·보수 이념과 무관하게, 자료 검토 후 온라인 의견 개진이나 조용한 투표를 통한 참여를 선호합니다.';
          }

          return { typeCode, axes, spectrum, spectrumLabel, spectrumDesc, ePct, partLabel, partDesc };
        }

        function renderHome() {
          return `
            <div class="wrap">
              <section class="section" style="padding-top:16px;">
                <p class="kicker">심리학 · 정치학 연구 기반 상관관계 설문 · 16문항</p>
                <h1>MBTI 인지 지표로 살펴보는<br/>나의 정치 · 사회적 가치관</h1>
                <p style="max-width:660px;margin:18px 0 0;font-size:15px;color:var(--sub);">
                  MBTI(성격 유형)와 정치 성향(진보·보수 등) 사이에는 통계적으로 유의미하지만 약한 수준의 상관관계가 존재합니다.
                  성격이 정치 태도를 완전히 결정하지는 않지만, 세상을 바라보는 인지 방식이 특정 가치관에 더 끌리게 만드는 경향을 16개 문항으로 점검합니다.
                </p>
                <div style="margin-top:26px;display:flex;flex-wrap:wrap;gap:12px;">
                  <button type="button" class="btn-primary" data-act="start">16문항 설문 시작하기 →</button>
                  <button type="button" class="btn-outline" data-act="home" data-sec="axes">4가지 지표 상관관계 보기</button>
                </div>
              </section>

              <section id="axes" class="section">
                <p class="kicker">핵심 지표별 상관관계 (빅5 · MBTI 연계 연구 기반)</p>
                <h2>네 가지 심리 축과 16개 문항 구성</h2>
                <div class="grid-2">
                  ${AXES.map(
                    (a, i) => `
                      <div class="card">
                        <div style="border-bottom:1px solid var(--border);padding-bottom:12px;">
                          <span class="mono" style="font-size:12px;color:var(--muted);">0${i + 1} · ${esc(a.sub)}</span>
                          <h3 class="serif" style="margin:4px 0 0;font-size:20px;">${esc(a.title)}</h3>
                        </div>
                        <div class="grid-2" style="margin-top:14px;gap:12px;">
                          <div class="sub-card">
                            <strong style="font-size:13px;"><span class="mono" style="color:var(--accent);">${a.left.letter}</span> · ${esc(a.left.name)}</strong>
                            <p style="margin:6px 0 0;font-size:12px;color:var(--sub);">${esc(a.left.desc)}</p>
                          </div>
                          <div class="sub-card">
                            <strong style="font-size:13px;"><span class="mono" style="color:var(--slate);">${a.right.letter}</span> · ${esc(a.right.name)}</strong>
                            <p style="margin:6px 0 0;font-size:12px;color:var(--sub);">${esc(a.right.desc)}</p>
                          </div>
                        </div>
                      </div>
                    `
                  ).join('')}
                </div>
              </section>
            </div>
          `;
        }

        function renderQuiz() {
          const q = QUESTIONS[state.idx];
          const answered = Object.keys(state.answers).length;
          const sel = state.answers[q.id];
          const allDone = answered === QUESTIONS.length;

          return `
            <div class="wrap-narrow">
              <div style="border-bottom:1px solid var(--border);padding-bottom:18px;">
                <div style="display:flex;justify-content:space-between;align-items:center;font-size:12px;color:var(--muted);">
                  <span><strong class="mono" style="color:var(--ink);">${String(state.idx + 1).padStart(2, '0')} / ${QUESTIONS.length}</strong> · ${esc(q.label)}</span>
                  <div style="display:flex;gap:14px;">
                    <button type="button" data-act="start">초기화</button>
                    <button type="button" data-act="home">나가기</button>
                  </div>
                </div>
                <div class="progress-bg">
                  <div class="progress-fill" style="transform:scaleX(${(state.idx + 1) / QUESTIONS.length});"></div>
                </div>
                <div class="steps">
                  ${QUESTIONS.map((item, i) => {
                    const isDone = state.answers[item.id] !== undefined;
                    const can = isDone || i <= answered;
                    return `<button type="button" class="step ${i === state.idx ? 'active' : isDone ? 'done' : ''}" ${can ? '' : 'disabled'} data-act="jump" data-idx="${i}">${String(item.id).padStart(2, '0')}</button>`;
                  }).join('')}
                </div>
              </div>

              <div style="padding-top:28px;">
                <p style="margin:0;font-size:12px;font-weight:600;color:var(--accent);">설문 장면 — ${esc(q.scene)}</p>
                <h2 style="font-size:clamp(1.4rem,2.6vw,1.75rem);margin-top:8px;">${esc(q.prompt)}</h2>

                <div class="grid-2">
                  <div class="card" style="padding:18px;border-color:${sel !== undefined && sel < 0 ? 'var(--accent)' : 'var(--border)'};">
                    <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--muted);">
                      <strong class="mono" style="color:var(--ink);">선택지 A</strong>
                      <span class="mono">${q.poleA} 지표</span>
                    </div>
                    <p style="margin:10px 0 0;font-size:14px;">${esc(q.textA)}</p>
                  </div>
                  <div class="card" style="padding:18px;border-color:${sel !== undefined && sel > 0 ? 'var(--slate)' : 'var(--border)'};">
                    <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--muted);">
                      <strong class="mono" style="color:var(--ink);">선택지 B</strong>
                      <span class="mono">${q.poleB} 지표</span>
                    </div>
                    <p style="margin:10px 0 0;font-size:14px;">${esc(q.textB)}</p>
                  </div>
                </div>

                <div style="margin-top:24px;">
                  <p style="margin:0;font-size:12px;color:var(--muted);">가장 가까운 태도를 선택하세요 (숫자키 <span class="mono">1–4</span> 지원)</p>
                  <div class="grid-4">
                    ${CHOICES.map(
                      (c) => `
                        <button type="button" class="choice ${sel === c.val ? 'selected' : ''}" data-act="choose" data-val="${c.val}">
                          <div style="display:flex;justify-content:space-between;width:100%;font-size:14px;font-weight:600;">
                            <span>${c.label}</span>
                            <span class="mono" style="font-size:12px;opacity:0.75;">[${c.key}]</span>
                          </div>
                          <span style="font-size:11px;opacity:0.85;">${c.sub}</span>
                        </button>
                      `
                    ).join('')}
                  </div>
                </div>
              </div>

              <div style="margin-top:32px;padding-top:20px;border-top:1px solid var(--border);display:flex;justify-content:space-between;">
                <button type="button" class="btn-outline" ${state.idx === 0 ? 'disabled style="opacity:0.4;cursor:not-allowed;"' : ''} data-act="prev">← 이전 문항</button>
                ${
                  allDone
                    ? `<button type="button" class="btn-primary" data-act="finish">결과 리포트 보기 →</button>`
                    : `<button type="button" class="btn-outline" ${sel === undefined || state.idx === QUESTIONS.length - 1 ? 'disabled style="opacity:0.4;cursor:not-allowed;"' : ''} data-act="next">다음 문항 →</button>`
                }
              </div>
            </div>
          `;
        }

        function renderResult() {
          const r = state.result;
          if (!r) return renderHome();
          const dotLeft = Math.min(96, Math.max(4, r.spectrum));

          return `
            <div class="wrap">
              <section class="section" style="padding-top:0;">
                <p class="kicker">MBTI × 정치 성향 설문 결과 리포트</p>
                <div style="display:flex;flex-wrap:wrap;align-items:baseline;gap:14px;margin-top:10px;">
                  <span class="mono" style="font-size:44px;font-weight:600;color:var(--accent);">${r.typeCode}</span>
                  <h1 style="margin:0;font-size:28px;">${esc(TYPE_TITLES[r.typeCode] || '')}</h1>
                </div>
                <p style="margin:12px 0 0;font-size:13px;color:var(--muted);">
                  ※ 본 결과는 성격 지표와 정치·가치관 사이의 약한 상관관계 연구를 바탕으로 한 경향 참고용 분석입니다.
                </p>
                <div style="margin-top:20px;display:flex;flex-wrap:wrap;gap:10px;">
                  <button type="button" class="btn-primary" data-act="copy">${state.copied ? '✓ 결과 요약 복사됨' : '결과 요약 복사하기'}</button>
                  <button type="button" class="btn-outline" data-act="start">다시 설문하기</button>
                </div>
              </section>

              <section class="section">
                <p class="kicker">이념 가치관 스펙트럼 & 참여 스타일</p>
                <h2>인지 지표에 따른 정치 성향 분포</h2>
                <div class="grid-2">
                  <div class="card">
                    <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--muted);">
                      <strong>가치관 스펙트럼 (S·T·J ↔ N·F·P)</strong>
                      <span class="mono">변화·공감·자율 비중 ${r.spectrum}%</span>
                    </div>
                    <h3 class="serif" style="margin:10px 0 0;font-size:20px;">${esc(r.spectrumLabel)}</h3>
                    <p style="margin:10px 0 0;font-size:14px;color:var(--sub);">${esc(r.spectrumDesc)}</p>
                    <div style="margin-top:20px;">
                      <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--muted);">
                        <span>보수 경향 (S·T·J)</span><span>중도 균형</span><span>진보 경향 (N·F·P)</span>
                      </div>
                      <div class="spectrum-track"><div class="spectrum-dot" style="left:${dotLeft}%;"></div></div>
                    </div>
                  </div>

                  <div class="card">
                    <div style="display:flex;justify-content:space-between;font-size:12px;color:var(--muted);">
                      <strong>정치 참여 방식 (E / I)</strong>
                      <span class="mono">외향(E) ${r.ePct}% · 내향(I) ${100 - r.ePct}%</span>
                    </div>
                    <h3 class="serif" style="margin:10px 0 0;font-size:20px;">${esc(r.partLabel)}</h3>
                    <p style="margin:10px 0 0;font-size:14px;color:var(--sub);">${esc(r.partDesc)}</p>
                    <p style="margin:14px 0 0;padding-top:10px;border-top:1px solid var(--border);font-size:12px;color:var(--muted);">
                      외향(E)과 내향(I)은 진보·보수 이념 방향 자체와는 거의 상관이 없으며 참여 행동 양식의 차이로 드러납니다.
                    </p>
                  </div>
                </div>
              </section>

              <section class="section">
                <p class="kicker">네 가지 지표별 16문항 응답 결과</p>
                <h2>세부 축 비율</h2>
                <div class="grid-2">
                  ${r.axes
                    .map((a) => {
                      const leftWin = a.winner === a.lPole;
                      return `
                        <div class="card">
                          <div style="display:flex;justify-content:space-between;align-items:center;font-size:13px;">
                            <strong>${esc(a.title)}</strong>
                            <span style="font-size:12px;color:var(--muted);">${a.close ? '고른 분포' : `${a.winner} 우세`}</span>
                          </div>
                          <div style="margin-top:12px;display:flex;justify-content:space-between;font-size:13px;">
                            <span style="${leftWin ? 'font-weight:600;' : 'color:var(--muted);'}"><span class="mono">${a.lPole}</span> · ${a.lName} <span class="mono">${a.lPct}%</span></span>
                            <span style="${!leftWin ? 'font-weight:600;' : 'color:var(--muted);'}"><span class="mono">${a.rPct}%</span> ${a.rName} · <span class="mono">${a.rPole}</span></span>
                          </div>
                          <div class="dual-bar">
                            <div style="width:${a.lPct}%;background:${leftWin ? 'var(--accent)' : '#d6d3d1'};"></div>
                            <div style="width:${a.rPct}%;background:${!leftWin ? 'var(--slate)' : '#d6d3d1'};"></div>
                          </div>
                        </div>
                      `;
                    })
                    .join('')}
                </div>
              </section>
            </div>
          `;
        }

        function render() {
          const app = document.getElementById('app');
          const btn = document.getElementById('header-start');
          btn.textContent = state.view === 'quiz' ? '설문 초기화' : '16문항 설문 시작';
          if (state.view === 'home') app.innerHTML = renderHome();
          else if (state.view === 'quiz') app.innerHTML = renderQuiz();
          else app.innerHTML = renderResult();
        }

        function choose(val) {
          const q = QUESTIONS[state.idx];
          state.answers[q.id] = val;
          render();
          setTimeout(() => {
            if (state.idx < QUESTIONS.length - 1) {
              state.idx += 1;
              render();
            } else {
              state.result = computeResult();
              state.view = 'result';
              window.scrollTo({ top: 0, behavior: 'smooth' });
              render();
            }
          }, 150);
        }

        document.addEventListener('click', (e) => {
          const el = e.target.closest('[data-act]');
          if (!el) return;
          const act = el.dataset.act;
          if (act === 'home') {
            state.view = 'home';
            render();
            if (el.dataset.sec) {
              setTimeout(() => {
                const target = document.getElementById(el.dataset.sec);
                if (target) target.scrollIntoView({ behavior: 'smooth' });
              }, 30);
            }
          } else if (act === 'start') {
            state.answers = {};
            state.idx = 0;
            state.copied = false;
            state.view = 'quiz';
            window.scrollTo({ top: 0, behavior: 'smooth' });
            render();
          } else if (act === 'choose') {
            choose(Number(el.dataset.val));
          } else if (act === 'jump') {
            state.idx = Number(el.dataset.idx);
            render();
          } else if (act === 'prev' && state.idx > 0) {
            state.idx -= 1;
            render();
          } else if (act === 'next' && state.idx < QUESTIONS.length - 1) {
            state.idx += 1;
            render();
          } else if (act === 'finish') {
            state.result = computeResult();
            state.view = 'result';
            window.scrollTo({ top: 0, behavior: 'smooth' });
            render();
          } else if (act === 'copy' && state.result) {
            const r = state.result;
            const summary = `[결 GYEOL · MBTI × 정치 성향 결과]\n유형: ${r.typeCode} (${TYPE_TITLES[r.typeCode]})\n가치관 스펙트럼: ${r.spectrumLabel}\n참여 방식: ${r.partLabel}`;
            if (navigator.clipboard && navigator.clipboard.writeText) {
              navigator.clipboard.writeText(summary).catch(() => {});
            }
            state.copied = true;
            render();
            setTimeout(() => { state.copied = false; render(); }, 2200);
          }
        });

        window.addEventListener('keydown', (e) => {
          if (state.view !== 'quiz') return;
          if (e.key === '1') choose(-2);
          else if (e.key === '2') choose(-1);
          else if (e.key === '3') choose(1);
          else if (e.key === '4') choose(2);
          else if (e.key === 'ArrowLeft' && state.idx > 0) {
            state.idx -= 1;
            render();
          }
        });

        render();
      })();
    </script>
  </body>
</html>Uploading ai_studio_code.html…]()
