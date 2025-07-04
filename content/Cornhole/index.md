---
title: "Cornhole Score Tracker"
draft: false
date: 2025-07-04
description: "Cornhole Score Tracker"
tags: ["cornhole", "tracker"]
showHero: false
---

<style>
/* Remove global html/body overrides to preserve theme layout */
.cornhole-container {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  font-family: sans-serif;
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.cornhole-section {
  flex: 1 1 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 32px 8px 24px 8px;
  justify-content: center;
  position: relative;
}
.cornhole-section.team1 {
  background: #e53935;
  color: #fff;
  border-top-left-radius: 16px;
  border-top-right-radius: 16px;
  padding-top: 16px;
}
.cornhole-section.team2 {
  background: #1e88e5;
  color: #fff;
  border-bottom-left-radius: 16px;
  border-bottom-right-radius: 16px;
  padding-top: 40px;
  padding-bottom: 24px;
}
.cornhole-title {
  font-size: 1.5em;
  font-weight: bold;
  margin-bottom: 16px;
}
.cornhole-btn-row {
  display: flex;
  gap: 12px;
  margin-bottom: 8px;
}
.cornhole-reset-row {
  display: flex;
  justify-content: center;
  margin-bottom: 16px;
}
.cornhole-btn {
  font-size: 1.2em;
  padding: 10px 18px;
  border: none;
  border-radius: 24px;
  background: #222;
  color: #fff !important;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
  transition: background 0.2s;
}
.cornhole-btn:active {
  background: #333;
}
.cornhole-reset-btn {
  margin-left: 0;
}
.cornhole-score-row {
  display: flex;
  flex-direction: row;
  gap: 32px;
  margin-bottom: 8px;
  width: 100%;
  max-width: 500px;
  justify-content: center;
}
.cornhole-score-col {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1 1 0;
}
.cornhole-label {
  font-size: 1em;
  margin-bottom: 2px;
}
.cornhole-score-box {
  width: 120px;
  font-size: 1.3em;
  text-align: center;
  padding: 8px 0;
  border-radius: 6px;
  background: #fff;
  color: #222;
  border: none;
  margin-bottom: 4px;
  pointer-events: none;
}
.cornhole-divider {
  width: 100%;
  height: 2px;
  background: #eee;
  position: relative;
  z-index: 1;
}
.cornhole-end-round-btn {
  position: absolute;
  left: 50%;
  top: 100%;
  transform: translate(-50%, -50%);
  z-index: 2;
  font-size: 1.1em;
  padding: 12px 28px;
  border-radius: 24px;
  background: #222;
  color: #fff;
  border: none;
  font-weight: bold;
  box-shadow: 0 2px 8px rgba(0,0,0,0.12);
  cursor: pointer;
  min-width: 140px;
  white-space: nowrap;
}
.cornhole-restart-btn {
  margin: 32px auto 0 auto;
  display: block;
  font-size: 1.1em;
  padding: 14px 32px;
  border-radius: 24px;
  background: #222;
  color: #fff;
  border: none;
  font-weight: bold;
  box-shadow: 0 2px 8px rgba(0,0,0,0.10);
  cursor: pointer;
}
@media (max-width: 600px) {
  .cornhole-container {
    padding: 0;
  }
  .cornhole-section {
    padding: 20px 4px 16px 4px;
  }
  .cornhole-end-round-btn {
    font-size: 1em;
    min-width: 0;
    padding: 10px 10px;
  }
  .cornhole-restart-btn {
    font-size: 1em;
    padding: 12px 12px;
  }
  .cornhole-score-row {
    gap: 8px;
    max-width: 220px;
  }
  .cornhole-score-box {
    width: 70px;
    font-size: 1.1em;
  }
}
.single .cover, .single .featured-image, .single .page-header__cover { display: none !important; }
</style>

<div class="cornhole-container">
  <!-- Team 1 Section -->
  <div class="cornhole-section team1">
    <div class="cornhole-title">Team 1</div>
    <div class="cornhole-btn-row">
      <button class="cornhole-btn">+1</button>
      <button class="cornhole-btn">+3</button>
    </div>
    <div class="cornhole-reset-row">
      <button class="cornhole-btn cornhole-reset-btn">Reset Round</button>
    </div>
    <div class="cornhole-score-row">
      <div class="cornhole-score-col">
        <label class="cornhole-label" for="team1-current">Current Round</label>
        <input class="cornhole-score-box" id="team1-current" type="text" value="0" readonly />
      </div>
      <div class="cornhole-score-col">
        <label class="cornhole-label" for="team1-overall">Overall Score</label>
        <input class="cornhole-score-box" id="team1-overall" type="text" value="0" readonly />
      </div>
    </div>
    <!-- End Round button overlaps divider -->
    <button class="cornhole-end-round-btn">End Round</button>
  </div>

  <!-- Divider -->
  <div class="cornhole-divider"></div>

  <!-- Team 2 Section -->
  <div class="cornhole-section team2">
    <div class="cornhole-title">Team 2</div>
    <div class="cornhole-btn-row">
      <button class="cornhole-btn">+1</button>
      <button class="cornhole-btn">+3</button>
    </div>
    <div class="cornhole-reset-row">
      <button class="cornhole-btn cornhole-reset-btn">Reset Round</button>
    </div>
    <div class="cornhole-score-row">
      <div class="cornhole-score-col">
        <label class="cornhole-label" for="team2-current">Current Round</label>
        <input class="cornhole-score-box" id="team2-current" type="text" value="0" readonly />
      </div>
      <div class="cornhole-score-col">
        <label class="cornhole-label" for="team2-overall">Overall Score</label>
        <input class="cornhole-score-box" id="team2-overall" type="text" value="0" readonly />
      </div>
    </div>
    <button class="cornhole-restart-btn">Restart Game</button>
  </div>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Team 1
  const team1Current = document.getElementById('team1-current');
  const team1Overall = document.getElementById('team1-overall');
  const team1Btns = document.querySelectorAll('.team1 .cornhole-btn');
  const team1Reset = document.querySelector('.team1 .cornhole-reset-btn');

  // Team 2
  const team2Current = document.getElementById('team2-current');
  const team2Overall = document.getElementById('team2-overall');
  const team2Btns = document.querySelectorAll('.team2 .cornhole-btn');
  const team2Reset = document.querySelector('.team2 .cornhole-reset-btn');

  // End Round & Restart
  const endRoundBtn = document.querySelector('.cornhole-end-round-btn');
  const restartBtn = document.querySelector('.cornhole-restart-btn');

  // Team 1: +1, +3
  team1Btns.forEach(btn => {
    if (btn.textContent === '+1') {
      btn.addEventListener('click', () => {
        team1Current.value = parseInt(team1Current.value, 10) + 1;
      });
    } else if (btn.textContent === '+3') {
      btn.addEventListener('click', () => {
        team1Current.value = parseInt(team1Current.value, 10) + 3;
      });
    }
  });
  // Team 1: Reset Round
  team1Reset.addEventListener('click', () => {
    team1Current.value = 0;
  });

  // Team 2: +1, +3
  team2Btns.forEach(btn => {
    if (btn.textContent === '+1') {
      btn.addEventListener('click', () => {
        team2Current.value = parseInt(team2Current.value, 10) + 1;
      });
    } else if (btn.textContent === '+3') {
      btn.addEventListener('click', () => {
        team2Current.value = parseInt(team2Current.value, 10) + 3;
      });
    }
  });
  // Team 2: Reset Round
  team2Reset.addEventListener('click', () => {
    team2Current.value = 0;
  });

  // End Round logic
  endRoundBtn.addEventListener('click', () => {
    const t1 = parseInt(team1Current.value, 10);
    const t2 = parseInt(team2Current.value, 10);
    if (t1 === t2) {
      // Tie: no points awarded
    } else if (t1 > t2) {
      team1Overall.value = parseInt(team1Overall.value, 10) + (t1 - t2);
    } else {
      team2Overall.value = parseInt(team2Overall.value, 10) + (t2 - t1);
    }
    team1Current.value = 0;
    team2Current.value = 0;
  });

  // Restart Game logic
  restartBtn.addEventListener('click', () => {
    team1Current.value = 0;
    team2Current.value = 0;
    team1Overall.value = 0;
    team2Overall.value = 0;
  });
});
</script> 