<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Alerta Violeta">
<meta name="theme-color" content="#1e1040">
<title>Alerta Violeta</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
:root {
  --purple: #6C3FC5; --purple-dark: #4B2A8A; --purple-light: #EDE8FB; --purple-mid: #9170D8;
  --text: #1a1a2e; --text-muted: #6b7280; --border: #e5e7eb; --bg: #f4f3f8; --white: #ffffff;
  --green: #2F855A; --green-bg: #F0FFF4; --amber: #D97706; --amber-bg: #FFFBEB;
  --red: #C53030; --red-bg: #FEF2F2;
  --radius: 14px;
  --safe-bottom: env(safe-area-inset-bottom, 0px);
  --safe-top: env(safe-area-inset-top, 0px);
}
html, body { height: 100%; overflow: hidden; font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif; background: var(--bg); color: var(--text); }

/* APP SHELL */
.app { display: flex; flex-direction: column; height: 100vh; height: 100dvh; }

/* TOP BAR */
.topbar {
  background: #1e1040;
  padding: calc(var(--safe-top) + 10px) 20px 10px;
  display: flex; align-items: center; justify-content: space-between;
  flex-shrink: 0; z-index: 50;
}
.topbar-brand { display: flex; align-items: center; gap: 10px; }
.logo-badge { width: 34px; height: 34px; background: var(--purple); border-radius: 9px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.logo-badge svg { width: 18px; height: 18px; fill: white; }
.logo-name { color: white; font-size: 17px; font-weight: 700; letter-spacing: -0.3px; }
.logo-sub { color: rgba(255,255,255,0.45); font-size: 10px; margin-top: 1px; }
.emergency-btn {
  display: flex; align-items: center; gap: 6px;
  background: var(--red); color: white; border: none; border-radius: 20px;
  padding: 7px 13px; font-size: 12px; font-weight: 700; cursor: pointer; font-family: inherit;
  text-decoration: none;
}
.emergency-btn::before { content: '🚨'; font-size: 13px; }

/* PAGES */
.pages { flex: 1; overflow-y: auto; overflow-x: hidden; -webkit-overflow-scrolling: touch; scroll-behavior: smooth; }
.page { display: none; min-height: 100%; padding: 20px 16px calc(80px + var(--safe-bottom)); }
.page.active { display: block; }

/* BOTTOM NAV */
.bottom-nav {
  flex-shrink: 0;
  background: white;
  border-top: 1px solid var(--border);
  display: flex;
  padding-bottom: var(--safe-bottom);
  z-index: 50;
}
.nav-item {
  flex: 1; display: flex; flex-direction: column; align-items: center;
  padding: 10px 4px 8px; gap: 3px; cursor: pointer;
  border: none; background: none; font-family: inherit; position: relative;
}
.nav-item .nav-icon { font-size: 22px; line-height: 1; transition: transform 0.15s; }
.nav-item .nav-label { font-size: 10px; color: var(--text-muted); font-weight: 500; }
.nav-item.active .nav-label { color: var(--purple); font-weight: 600; }
.nav-item.active .nav-icon { transform: scale(1.12); }
.nav-item.active::after {
  content: ''; position: absolute; top: 0; left: 25%; right: 25%;
  height: 2px; background: var(--purple); border-radius: 0 0 2px 2px;
}

/* HOME */
.hero-card {
  background: linear-gradient(135deg, #1e1040 0%, #3d1f7a 100%);
  border-radius: var(--radius); padding: 24px 20px; margin-bottom: 16px; position: relative; overflow: hidden;
}
.hero-card::before {
  content: ''; position: absolute; width: 180px; height: 180px;
  background: rgba(255,255,255,0.04); border-radius: 50%;
  right: -40px; top: -40px;
}
.hero-card::after {
  content: ''; position: absolute; width: 120px; height: 120px;
  background: rgba(255,255,255,0.04); border-radius: 50%;
  right: 30px; bottom: -30px;
}
.hero-emoji { font-size: 36px; margin-bottom: 10px; }
.hero-card h1 { color: white; font-size: 20px; font-weight: 700; margin-bottom: 6px; line-height: 1.3; }
.hero-card p { color: rgba(255,255,255,0.7); font-size: 13px; line-height: 1.6; margin-bottom: 16px; }
.btn-hero {
  display: inline-flex; align-items: center; gap: 8px;
  background: white; color: var(--purple-dark);
  border: none; border-radius: 10px; padding: 11px 18px;
  font-size: 14px; font-weight: 700; cursor: pointer; font-family: inherit;
}
.emergency-strip {
  background: var(--red-bg); border: 1px solid #FECACA; border-radius: var(--radius);
  padding: 14px 16px; display: flex; align-items: center; gap: 12px; margin-bottom: 16px;
}
.emergency-strip .ei { font-size: 24px; }
.emergency-strip strong { font-size: 13px; color: var(--red); display: block; margin-bottom: 3px; }
.emergency-strip p { font-size: 12px; color: #7f1d1d; line-height: 1.4; }
.emergency-strip a { color: var(--red); font-weight: 700; text-decoration: none; }
.section-title { font-size: 14px; font-weight: 700; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 10px; }
.quick-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.quick-card {
  background: white; border: 1px solid var(--border); border-radius: var(--radius);
  padding: 16px 14px; cursor: pointer; transition: all 0.15s; display: flex; flex-direction: column; gap: 6px;
  -webkit-user-select: none; user-select: none;
}
.quick-card:active { background: var(--purple-light); border-color: var(--purple-mid); transform: scale(0.98); }
.quick-card .qi { font-size: 26px; }
.quick-card h3 { font-size: 14px; font-weight: 600; }
.quick-card p { font-size: 12px; color: var(--text-muted); line-height: 1.4; }

/* PAGE HEADER */
.page-header { margin-bottom: 20px; }
.page-header h2 { font-size: 22px; font-weight: 700; margin-bottom: 6px; }
.page-header p { font-size: 14px; color: var(--text-muted); line-height: 1.6; }

/* CARDS */
.card { background: white; border-radius: var(--radius); border: 1px solid var(--border); padding: 20px 18px; }
.card + .card { margin-top: 12px; }

/* FORM */
.form-block { display: flex; flex-direction: column; gap: 18px; }
.field { display: flex; flex-direction: column; gap: 6px; }
.field label { font-size: 13px; font-weight: 600; color: var(--text); }
.field input, .field select, .field textarea {
  border: 1.5px solid var(--border); border-radius: 10px; padding: 12px 14px;
  font-size: 15px; font-family: inherit; color: var(--text); outline: none;
  width: 100%; transition: border-color 0.15s; background: white;
  -webkit-appearance: none; appearance: none;
}
.field input:focus, .field select:focus, .field textarea:focus {
  border-color: var(--purple); box-shadow: 0 0 0 3px rgba(108,63,197,0.12);
}
.field textarea { resize: none; min-height: 100px; line-height: 1.6; }
.select-wrap { position: relative; }
.select-wrap::after {
  content: ''; position: absolute; right: 14px; top: 50%;
  transform: translateY(-50%); border: 5px solid transparent;
  border-top-color: var(--text-muted); margin-top: 3px; pointer-events: none;
}
.field-note { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
.type-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; }
.type-btn {
  display: flex; flex-direction: column; align-items: center; gap: 6px;
  padding: 12px 8px; border: 1.5px solid var(--border); border-radius: 12px;
  background: white; cursor: pointer; font-family: inherit; transition: all 0.15s;
}
.type-btn:active, .type-btn.selected { border-color: var(--purple); background: var(--purple-light); }
.type-btn .icon { font-size: 24px; }
.type-btn span { font-size: 11px; color: var(--text); font-weight: 500; text-align: center; line-height: 1.3; }
.radio-group, .checkbox-group { display: flex; flex-direction: column; gap: 10px; }
.radio-label, .checkbox-label {
  display: flex; align-items: center; gap: 12px; font-size: 15px;
  cursor: pointer; padding: 10px 14px; border: 1.5px solid var(--border);
  border-radius: 10px; background: white; transition: all 0.15s;
}
.radio-label input, .checkbox-label input { width: 20px; height: 20px; accent-color: var(--purple); cursor: pointer; flex-shrink: 0; }
.radio-label:has(input:checked), .checkbox-label:has(input:checked) { border-color: var(--purple); background: var(--purple-light); }
.toggle-row { display: flex; align-items: center; justify-content: space-between; gap: 16px; padding: 12px 0; }
.toggle-row span { font-size: 15px; }
.toggle { position: relative; display: inline-block; width: 52px; height: 28px; flex-shrink: 0; }
.toggle input { opacity: 0; width: 0; height: 0; }
.toggle-slider { position: absolute; inset: 0; background: #d1d5db; border-radius: 28px; cursor: pointer; transition: 0.2s; }
.toggle-slider::after { content:''; position: absolute; width: 22px; height: 22px; border-radius: 50%; background: white; left: 3px; top: 3px; transition: 0.2s; box-shadow: 0 1px 4px rgba(0,0,0,0.2); }
.toggle input:checked + .toggle-slider { background: var(--purple); }
.toggle input:checked + .toggle-slider::after { transform: translateX(24px); }
.divider { height: 1px; background: var(--border); }
.btn-primary {
  display: flex; align-items: center; justify-content: center; gap: 10px;
  background: var(--purple); color: white; border: none; border-radius: 12px;
  padding: 15px 24px; font-size: 16px; font-weight: 700; cursor: pointer; font-family: inherit;
  width: 100%; transition: background 0.15s; -webkit-user-select: none; user-select: none;
}
.btn-primary:active { background: var(--purple-dark); }
.anon-badge {
  display: flex; align-items: center; gap: 10px;
  background: var(--green-bg); border: 1px solid #C6F6D5; border-radius: 10px;
  padding: 12px 14px; font-size: 13px; color: var(--green);
}
.anon-badge span { font-size: 18px; flex-shrink: 0; }

/* CHAT */
.chat-window { background: white; border-radius: var(--radius); border: 1px solid var(--border); display: flex; flex-direction: column; height: 420px; overflow: hidden; }
.chat-header { padding: 14px 16px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 10px; }
.chat-avatar { width: 36px; height: 36px; border-radius: 50%; background: var(--purple-light); display: flex; align-items: center; justify-content: center; font-size: 18px; flex-shrink: 0; }
.chat-online { display: flex; align-items: center; gap: 5px; font-size: 12px; color: var(--green); }
.chat-online::before { content:''; width: 7px; height: 7px; border-radius: 50%; background: var(--green); }
.chat-messages { flex: 1; overflow-y: auto; padding: 16px; display: flex; flex-direction: column; gap: 12px; -webkit-overflow-scrolling: touch; }
.msg { max-width: 82%; }
.msg.bot { align-self: flex-start; }
.msg.user { align-self: flex-end; }
.msg-bubble { padding: 10px 14px; border-radius: 16px; font-size: 14px; line-height: 1.5; }
.msg.bot .msg-bubble { background: var(--purple-light); color: var(--text); border-bottom-left-radius: 4px; }
.msg.user .msg-bubble { background: var(--purple); color: white; border-bottom-right-radius: 4px; }
.msg-time { font-size: 11px; color: var(--text-muted); margin-top: 4px; }
.msg.user .msg-time { text-align: right; }
.chat-input-area { border-top: 1px solid var(--border); padding: 10px 12px; display: flex; gap: 8px; align-items: flex-end; }
.chat-input-area textarea { flex: 1; border: 1.5px solid var(--border); border-radius: 10px; padding: 10px 12px; font-size: 14px; font-family: inherit; resize: none; outline: none; max-height: 100px; min-height: 40px; line-height: 1.5; }
.chat-input-area textarea:focus { border-color: var(--purple); }
.chat-send { width: 40px; height: 40px; border-radius: 10px; background: var(--purple); border: none; cursor: pointer; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.chat-send svg { width: 17px; height: 17px; stroke: white; }

/* TRACKING */
.search-row { display: flex; gap: 8px; margin-bottom: 16px; }
.search-row input { flex: 1; border: 1.5px solid var(--border); border-radius: 10px; padding: 12px 14px; font-size: 15px; font-family: inherit; outline: none; -webkit-appearance: none; }
.search-row input:focus { border-color: var(--purple); }
.search-row button { background: var(--purple); color: white; border: none; border-radius: 10px; padding: 12px 16px; font-size: 14px; font-weight: 600; cursor: pointer; font-family: inherit; white-space: nowrap; }
.protocol-card { background: var(--purple-light); border: 1px solid rgba(108,63,197,0.2); border-radius: var(--radius); padding: 18px 20px; margin-bottom: 16px; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 12px; }
.protocol-card .pcode { font-size: 20px; font-weight: 700; color: var(--purple); letter-spacing: 1px; }
.protocol-card .plabel { font-size: 12px; color: var(--purple-dark); margin-bottom: 4px; }
.status-badge { display: inline-flex; align-items: center; gap: 5px; padding: 5px 13px; border-radius: 20px; font-size: 12px; font-weight: 600; }
.badge-green { background: var(--green-bg); color: var(--green); }
.badge-amber { background: var(--amber-bg); color: var(--amber); }
.badge-gray { background: #f3f4f6; color: #6b7280; }
.badge-purple { background: var(--purple-light); color: var(--purple); }
.timeline { display: flex; flex-direction: column; gap: 0; }
.timeline-item { display: flex; gap: 14px; padding-bottom: 24px; position: relative; }
.timeline-item:last-child { padding-bottom: 0; }
.timeline-left { display: flex; flex-direction: column; align-items: center; width: 32px; flex-shrink: 0; }
.timeline-dot { width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.timeline-dot.done { background: var(--green-bg); color: var(--green); }
.timeline-dot.active { background: var(--purple-light); color: var(--purple); }
.timeline-dot.pending { background: #f3f4f6; color: #9ca3af; }
.timeline-dot svg { width: 16px; height: 16px; }
.timeline-line { flex: 1; width: 2px; background: var(--border); margin-top: 4px; }
.timeline-item:last-child .timeline-line { display: none; }
.timeline-body { flex: 1; padding-top: 4px; }
.timeline-title { font-size: 14px; font-weight: 600; margin-bottom: 4px; display: flex; flex-wrap: wrap; align-items: center; gap: 6px; }
.timeline-desc { font-size: 13px; color: var(--text-muted); line-height: 1.5; }
.timeline-date { font-size: 12px; color: var(--text-muted); margin-top: 5px; }

/* RIGHTS */
.right-item { background: white; border: 1px solid var(--border); border-radius: var(--radius); padding: 16px 18px; display: flex; gap: 14px; align-items: flex-start; }
.right-item + .right-item { margin-top: 10px; }
.right-icon { width: 44px; height: 44px; border-radius: 12px; background: var(--purple-light); display: flex; align-items: center; justify-content: center; flex-shrink: 0; font-size: 22px; }
.right-body h3 { font-size: 14px; font-weight: 700; margin-bottom: 5px; }
.right-body p { font-size: 13px; color: var(--text-muted); line-height: 1.6; }
.right-law { font-size: 12px; color: var(--purple); font-weight: 500; margin-top: 5px; }

/* FAQ */
.faq-item { background: white; border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; margin-bottom: 8px; }
.faq-question { width: 100%; text-align: left; padding: 15px 16px; display: flex; align-items: center; justify-content: space-between; gap: 10px; background: white; border: none; cursor: pointer; font-family: inherit; font-size: 14px; font-weight: 500; }
.faq-question.open { color: var(--purple); }
.faq-arrow { width: 20px; height: 20px; flex-shrink: 0; transition: transform 0.2s; color: var(--text-muted); }
.faq-question.open .faq-arrow { transform: rotate(180deg); color: var(--purple); }
.faq-answer { display: none; padding: 0 16px 16px; font-size: 13px; color: var(--text-muted); line-height: 1.7; }
.faq-answer.open { display: block; }

/* QUIZ */
.quiz-q { font-size: 15px; font-weight: 600; margin-bottom: 14px; line-height: 1.5; }
.quiz-options { display: flex; flex-direction: column; gap: 8px; }
.quiz-opt { padding: 13px 15px; border: 1.5px solid var(--border); border-radius: 10px; cursor: pointer; font-size: 14px; transition: all 0.15s; background: white; font-family: inherit; text-align: left; }
.quiz-opt:active { background: var(--purple-light); }
.quiz-opt.selected { border-color: var(--purple); background: var(--purple-light); color: var(--purple-dark); font-weight: 500; }
.quiz-opt.correct { border-color: var(--green); background: var(--green-bg); color: var(--green); font-weight: 500; }
.quiz-opt.wrong { border-color: var(--red); background: var(--red-bg); color: var(--red); }
.quiz-feedback { margin-top: 12px; padding: 11px 14px; border-radius: 8px; font-size: 13px; line-height: 1.5; display: none; }
.quiz-feedback.show { display: block; }
.quiz-feedback.correct { background: var(--green-bg); color: var(--green); }
.quiz-feedback.wrong { background: var(--red-bg); color: var(--red); }
.quiz-nav { display: flex; justify-content: space-between; align-items: center; margin-top: 16px; }
.quiz-progress { font-size: 13px; color: var(--text-muted); }
.quiz-progress span { font-weight: 700; color: var(--purple); }
.btn-secondary { display: inline-flex; align-items: center; gap: 8px; background: white; color: var(--text); border: 1.5px solid var(--border); border-radius: 10px; padding: 10px 18px; font-size: 14px; font-weight: 600; cursor: pointer; font-family: inherit; }
.btn-secondary:disabled { opacity: 0.4; cursor: not-allowed; }
.quiz-result { text-align: center; padding: 16px 0; }
.quiz-result .trophy { font-size: 48px; }
.quiz-result .score { font-size: 42px; font-weight: 700; color: var(--purple); margin: 12px 0 6px; }

/* CONTACT */
.contact-card { background: white; border: 1px solid var(--border); border-radius: var(--radius); padding: 20px 18px; margin-bottom: 10px; display: flex; align-items: center; gap: 16px; }
.contact-num { font-size: 32px; font-weight: 700; color: var(--purple); flex-shrink: 0; width: 72px; text-align: center; }
.contact-body { flex: 1; }
.contact-body h3 { font-size: 14px; font-weight: 700; margin-bottom: 4px; }
.contact-body p { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
.call-badge { font-size: 11px; padding: 3px 10px; border-radius: 20px; font-weight: 600; display: inline-block; margin-bottom: 5px; }
.call-badge.green { background: var(--green-bg); color: var(--green); }
.call-badge.red { background: var(--red-bg); color: var(--red); }
.btn-call { display: flex; align-items: center; justify-content: center; gap: 6px; width: 100%; padding: 11px; border: none; border-radius: 10px; background: var(--purple); color: white; font-size: 14px; font-weight: 700; cursor: pointer; font-family: inherit; text-decoration: none; margin-top: 10px; }
.btn-call.red { background: var(--red); }
.btn-call.green { background: var(--green); }
.btn-call svg { width: 16px; height: 16px; }
.whatsapp-strip { background: #25D366; border-radius: var(--radius); padding: 16px 18px; display: flex; align-items: center; gap: 14px; text-decoration: none; margin-bottom: 10px; }
.whatsapp-strip svg { width: 32px; height: 32px; fill: white; flex-shrink: 0; }
.whatsapp-strip h3 { color: white; font-size: 14px; font-weight: 700; }
.whatsapp-strip p { color: rgba(255,255,255,0.85); font-size: 12px; margin-top: 2px; }
.schedule-item { display: flex; justify-content: space-between; align-items: center; padding: 11px 0; border-bottom: 1px solid var(--border); font-size: 13px; }
.schedule-item:last-child { border-bottom: none; }
.schedule-item .day { font-weight: 500; }
.schedule-item .hours { color: var(--text-muted); }

/* OVERLAY */
.success-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.55); z-index: 200; align-items: flex-end; justify-content: center; padding-bottom: var(--safe-bottom); }
.success-overlay.show { display: flex; }
.success-card { background: white; border-radius: 20px 20px 0 0; padding: 28px 24px 32px; width: 100%; max-width: 480px; animation: slideUp 0.3s ease; }
@keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
.success-icon { width: 64px; height: 64px; border-radius: 50%; background: var(--purple-light); display: flex; align-items: center; justify-content: center; margin: 0 auto 16px; font-size: 32px; }
.success-card h2 { font-size: 20px; text-align: center; margin-bottom: 8px; }
.success-card p { font-size: 13px; color: var(--text-muted); line-height: 1.6; text-align: center; }
.success-code { margin: 14px 0; padding: 12px; background: var(--purple-light); border-radius: 10px; font-size: 13px; color: var(--purple-dark); font-weight: 700; text-align: center; }
.btn-close { margin-top: 12px; padding: 13px; background: var(--purple); color: white; border: none; border-radius: 12px; font-size: 15px; font-weight: 700; cursor: pointer; font-family: inherit; width: 100%; }

/* VIDEO */
.video-card { background: white; border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; margin-bottom: 12px; }
.video-thumb { width: 100%; aspect-ratio: 16/9; background: #1e1040; display: flex; align-items: center; justify-content: center; position: relative; cursor: pointer; }
.play-btn { width: 50px; height: 50px; border-radius: 50%; background: rgba(255,255,255,0.15); border: 2px solid white; display: flex; align-items: center; justify-content: center; backdrop-filter: blur(4px); }
.play-btn svg { width: 20px; height: 20px; fill: white; margin-left: 3px; }
.video-info { padding: 14px 16px; }
.video-tag { font-size: 11px; font-weight: 700; color: var(--purple); background: var(--purple-light); padding: 3px 10px; border-radius: 20px; display: inline-block; margin-bottom: 8px; }
.video-info h3 { font-size: 14px; font-weight: 600; margin-bottom: 5px; line-height: 1.4; }
.video-info p { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
.video-duration { font-size: 11px; color: var(--text-muted); margin-top: 6px; }

/* SECTION SPACER */
.section-gap { height: 20px; }
</style>
</head>
<body>
<div class="app">

  <!-- TOP BAR -->
  <header class="topbar">
    <div class="topbar-brand">
      <div class="logo-badge">
        <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 14.5v-9l6 4.5-6 4.5z"/></svg>
      </div>
      <div>
        <div class="logo-name">alerta violeta</div>
        <div class="logo-sub">Seguro · Sigiloso · Acolhedor</div>
      </div>
    </div>
    <a href="tel:190" class="emergency-btn">190</a>
  </header>

  <!-- PAGES -->
  <div class="pages" id="pages">

    <!-- HOME -->
    <div class="page active" id="page-inicio">
      <div class="hero-card">
        <div class="hero-emoji">💜</div>
        <h1>Bem-vinda ao Alerta Violeta</h1>
        <p>Espaço seguro, sigiloso e acolhedor. Você não está sozinha.</p>
        <button class="btn-hero" onclick="goPage('denuncia','nav-denuncia')">
          📝 Fazer denúncia agora
        </button>
      </div>
      <div class="emergency-strip">
        <div class="ei">🚨</div>
        <div>
          <strong>Em perigo agora?</strong>
          <p>Ligue <a href="tel:190">190 (Polícia)</a> ou <a href="tel:192">192 (SAMU)</a> imediatamente.</p>
        </div>
      </div>
      <div class="section-title">Acesso rápido</div>
      <div class="quick-grid">
        <div class="quick-card" onclick="goPage('denuncia','nav-denuncia')">
          <div class="qi">📝</div>
          <h3>Fazer denúncia</h3>
          <p>Registre o que aconteceu com segurança</p>
        </div>
        <div class="quick-card" onclick="goPage('acompanhar','nav-mais')">
          <div class="qi">🔍</div>
          <h3>Acompanhar</h3>
          <p>Veja o andamento da sua denúncia</p>
        </div>
        <div class="quick-card" onclick="goPage('apoio','nav-apoio')">
          <div class="qi">💜</div>
          <h3>Buscar apoio</h3>
          <p>Vídeos e orientações</p>
        </div>
        <div class="quick-card" onclick="goPage('direitos','nav-mais')">
          <div class="qi">⚖️</div>
          <h3>Seus direitos</h3>
          <p>Leis que te protegem</p>
        </div>
        <div class="quick-card" onclick="goPage('faq','nav-mais')">
          <div class="qi">❓</div>
          <h3>Dúvidas</h3>
          <p>Perguntas frequentes</p>
        </div>
        <div class="quick-card" onclick="goPage('contato','nav-contato')">
          <div class="qi">📞</div>
          <h3>Contato</h3>
          <p>Fale com nossa equipe</p>
        </div>
      </div>
    </div>

    <!-- DENÚNCIA -->
    <div class="page" id="page-denuncia">
      <div class="page-header">
        <h2>Fazer denúncia</h2>
        <p>Registre pelo chat ou pelo formulário. Tudo com total sigilo.</p>
      </div>

      <div class="anon-badge" style="margin-bottom:16px;">
        <span>🔒</span> Sua identidade é 100% protegida. Nenhum dado pessoal é coletado.
      </div>

      <!-- CHAT -->
      <div class="card" style="padding:0;margin-bottom:16px;">
        <div class="chat-window">
          <div class="chat-header">
            <div class="chat-avatar">💜</div>
            <div style="flex:1;">
              <div style="font-size:14px;font-weight:600;">Equipe Alerta Violeta</div>
              <div class="chat-online">Online agora</div>
            </div>
          </div>
          <div class="chat-messages" id="chatMessages">
            <div class="msg bot">
              <div class="msg-bubble">Olá! Bem-vinda ao Alerta Violeta. 💜 Estamos aqui para te ouvir com total sigilo. Como posso te ajudar?</div>
              <div class="msg-time">Agora</div>
            </div>
            <div class="msg bot">
              <div class="msg-bubble">Pode me contar o que aconteceu com suas próprias palavras. Estamos aqui com você.</div>
              <div class="msg-time">Agora</div>
            </div>
          </div>
          <div class="chat-input-area">
            <textarea id="chatInput" placeholder="Escreva aqui..." rows="1" onkeydown="chatKeyDown(event)" oninput="autoResize(this)"></textarea>
            <button class="chat-send" onclick="sendChat()">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22,2 15,22 11,13 2,9"/></svg>
            </button>
          </div>
        </div>
      </div>

      <!-- FORM -->
      <div class="card">
        <div style="font-size:15px;font-weight:700;margin-bottom:4px;">Ou preencha o formulário</div>
        <div style="font-size:13px;color:var(--text-muted);margin-bottom:18px;">Prefere mais detalhes? Use o formulário abaixo.</div>

        <div class="form-block">
          <div class="field">
            <label>1. Tipo de situação</label>
            <div class="type-grid">
              <button class="type-btn" onclick="selectType(this)"><div class="icon">🤚</div><span>Abuso sexual</span></button>
              <button class="type-btn" onclick="selectType(this)"><div class="icon">🧑</div><span>Assédio</span></button>
              <button class="type-btn" onclick="selectType(this)"><div class="icon">✊</div><span>Agressão física</span></button>
              <button class="type-btn" onclick="selectType(this)"><div class="icon">🧠</div><span>Abuso psicológico</span></button>
              <button class="type-btn" onclick="selectType(this)"><div class="icon">👥</div><span>Discriminação</span></button>
              <button class="type-btn" onclick="selectType(this)"><div class="icon">•••</div><span>Outros</span></button>
            </div>
          </div>

          <div class="divider"></div>

          <div class="field">
            <label>2. Onde aconteceu?</label>
            <input type="text" placeholder="Ex.: Escola, trabalho, rua, casa...">
          </div>

          <div class="field">
            <label>3. Quando aconteceu?</label>
            <div class="select-wrap">
              <select>
                <option value="">Selecione</option>
                <option>Hoje</option>
                <option>Ontem</option>
                <option>Nesta semana</option>
                <option>Neste mês</option>
                <option>Há mais de um mês</option>
                <option>Prefiro não informar</option>
              </select>
            </div>
          </div>

          <div class="divider"></div>

          <div class="field">
            <label>4. A vítima está em risco agora?</label>
            <div class="radio-group">
              <label class="radio-label"><input type="radio" name="risco" value="sim"> Sim</label>
              <label class="radio-label"><input type="radio" name="risco" value="nao"> Não</label>
              <label class="radio-label"><input type="radio" name="risco" value="ns"> Não sei</label>
            </div>
          </div>

          <div class="field">
            <label>5. Quem sofreu?</label>
            <div class="radio-group">
              <label class="radio-label"><input type="radio" name="vitima" value="eu"> Eu</label>
              <label class="radio-label"><input type="radio" name="vitima" value="outra"> Outra pessoa</label>
              <label class="radio-label"><input type="radio" name="vitima" value="ni"> Prefiro não informar</label>
            </div>
          </div>

          <div class="divider"></div>

          <div class="field">
            <label>6. Descreva o que aconteceu (opcional)</label>
            <textarea placeholder="Conte com suas palavras o que aconteceu."></textarea>
          </div>

          <div class="field">
            <label>7. Existem evidências?</label>
            <div class="checkbox-group">
              <label class="checkbox-label"><input type="checkbox"> Sim (fotos, vídeos, áudios)</label>
              <label class="checkbox-label"><input type="checkbox"> Não tenho provas</label>
              <label class="checkbox-label"><input type="checkbox"> Não sei</label>
            </div>
          </div>

          <div class="divider"></div>

          <div class="field">
            <label>8. Anonimato</label>
            <div class="toggle-row">
              <span>Quero permanecer anônima 🔒</span>
              <label class="toggle"><input type="checkbox" checked><span class="toggle-slider"></span></label>
            </div>
            <div class="field-note">Seus dados estarão totalmente protegidos.</div>
          </div>

          <button class="btn-primary" onclick="submitForm()">
            Enviar denúncia 💜
          </button>

          <div class="anon-badge">
            <span>🛡️</span> Ao enviar, suas informações são protegidas por criptografia.
          </div>
        </div>
      </div>
    </div>

    <!-- APOIO -->
    <div class="page" id="page-apoio">
      <div class="page-header">
        <h2>Informações e apoio</h2>
        <p>Vídeos educativos para orientar você sobre como agir e buscar ajuda.</p>
      </div>

      <div class="video-card">
        <div class="video-thumb" onclick="openVideo('https://www.youtube.com/embed/XpUzBtJzoQI',this)">
          <div style="width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-size:48px;">📞</div>
          <div class="play-btn"><svg viewBox="0 0 24 24"><polygon points="5,3 19,12 5,21"/></svg></div>
        </div>
        <div class="video-info">
          <span class="video-tag">Como denunciar</span>
          <h3>Vídeo 1</h3>
          <p>Toque para assistir.</p>
        </div>
      </div>

      <div class="video-card">
        <div class="video-thumb" onclick="openVideo('https://www.youtube.com/embed/NuCYWf6NlAM',this)">
          <div style="width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-size:48px;">⚖️</div>
          <div class="play-btn"><svg viewBox="0 0 24 24"><polygon points="5,3 19,12 5,21"/></svg></div>
        </div>
        <div class="video-info">
          <span class="video-tag">Direitos</span>
          <h3>Vídeo 2</h3>
          <p>Toque para assistir.</p>
        </div>
      </div>

      <div class="video-card">
        <div class="video-thumb" onclick="openVideo('https://www.youtube.com/embed/0KkYoKK8TMk',this)">
          <div style="width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-size:48px;">🏥</div>
          <div class="play-btn"><svg viewBox="0 0 24 24"><polygon points="5,3 19,12 5,21"/></svg></div>
        </div>
        <div class="video-info">
          <span class="video-tag">Saúde</span>
          <h3>Vídeo 3</h3>
          <p>Toque para assistir.</p>
        </div>
      </div>

      <div class="video-card">
        <div class="video-thumb" onclick="openVideo('https://www.youtube.com/embed/CJi-0sS0bAk',this)">
          <div style="width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-size:48px;">💆</div>
          <div class="play-btn"><svg viewBox="0 0 24 24"><polygon points="5,3 19,12 5,21"/></svg></div>
        </div>
        <div class="video-info">
          <span class="video-tag">Saúde mental</span>
          <h3>Vídeo 4</h3>
          <p>Toque para assistir.</p>
        </div>
      </div>
    </div>

    <!-- CONTATO -->
    <div class="page" id="page-contato">
      <div class="page-header">
        <h2>Contato e emergências</h2>
        <p>Escolha o canal de atendimento que preferir.</p>
      </div>

      <a href="https://api.whatsapp.com/send?phone=5511999999999" class="whatsapp-strip">
        <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
        <div>
          <h3>WhatsApp — Alerta Violeta</h3>
          <p>Seg–Sex, 8h às 20h · Sab 9h–13h</p>
        </div>
      </a>

      <div class="contact-card">
        <div>
          <div class="call-badge green">● Gratuito · 24h</div>
          <div class="contact-num">180</div>
        </div>
        <div class="contact-body">
          <h3>Central da Mulher</h3>
          <p>Denúncia, informação e orientação. Sigiloso e gratuito.</p>
          <a href="tel:180" class="btn-call">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-5.99-5.99 19.79 19.79 0 01-3.07-8.68A2 2 0 012 1h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L6.91 8.1a16 16 0 006 6l.38-.38a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z"/></svg>
            Ligar 180
          </a>
        </div>
      </div>

      <div class="contact-card">
        <div>
          <div class="call-badge red">● Emergência</div>
          <div class="contact-num" style="color:var(--red)">190</div>
        </div>
        <div class="contact-body">
          <h3>Polícia Militar</h3>
          <p>Perigo imediato ou flagrante delito.</p>
          <a href="tel:190" class="btn-call red">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-5.99-5.99 19.79 19.79 0 01-3.07-8.68A2 2 0 012 1h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L6.91 8.1a16 16 0 006 6l.38-.38a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z"/></svg>
            Ligar 190
          </a>
        </div>
      </div>

      <div class="contact-card">
        <div>
          <div class="call-badge green">● Gratuito</div>
          <div class="contact-num">181</div>
        </div>
        <div class="contact-body">
          <h3>Disque-Denúncia</h3>
          <p>Anônimo para qualquer tipo de crime.</p>
          <a href="tel:181" class="btn-call">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-5.99-5.99 19.79 19.79 0 01-3.07-8.68A2 2 0 012 1h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L6.91 8.1a16 16 0 006 6l.38-.38a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z"/></svg>
            Ligar 181
          </a>
        </div>
      </div>

      <div class="contact-card">
        <div>
          <div class="call-badge green">● Apoio emocional</div>
          <div class="contact-num" style="color:var(--green)">188</div>
        </div>
        <div class="contact-body">
          <h3>CVV</h3>
          <p>Sofrimento emocional. Voluntário e sigiloso, 24h.</p>
          <a href="tel:188" class="btn-call green">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-5.99-5.99 19.79 19.79 0 01-3.07-8.68A2 2 0 012 1h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L6.91 8.1a16 16 0 006 6l.38-.38a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z"/></svg>
            Ligar 188
          </a>
        </div>
      </div>

      <div class="card" style="margin-top:4px;">
        <div style="font-size:14px;font-weight:700;margin-bottom:12px;">📅 Horário — Equipe Alerta Violeta</div>
        <div class="schedule-item"><span class="day">Segunda a Sexta</span><span class="hours">08:00 – 20:00</span><span class="status-badge badge-green" style="font-size:11px;">Disponível</span></div>
        <div class="schedule-item"><span class="day">Sábado</span><span class="hours">09:00 – 13:00</span><span class="status-badge badge-amber" style="font-size:11px;">Limitado</span></div>
        <div class="schedule-item"><span class="day">Domingo e feriados</span><span class="hours">—</span><span class="status-badge badge-gray" style="font-size:11px;">Fechado</span></div>
        <div style="font-size:12px;color:var(--text-muted);margin-top:10px;">⚠️ Fora do horário, ligue 180 ou 190. Funcionamento 24h.</div>
      </div>
    </div>

    <!-- MAIS (hub) -->
    <div class="page" id="page-mais">
      <div class="page-header">
        <h2>Mais opções</h2>
      </div>

      <!-- ACOMPANHAR -->
      <div class="section-title">🔍 Acompanhar denúncia</div>
      <div class="card" style="margin-bottom:20px;">
        <div style="font-size:13px;color:var(--text-muted);margin-bottom:12px;">Insira o número do protocolo recebido ao enviar sua denúncia.</div>
        <div class="search-row">
          <input type="text" id="protocolInput" placeholder="Ex: AV-849302">
          <button onclick="buscarProtocolo()">Buscar</button>
        </div>
        <div id="trackingResult" style="display:none;">
          <div class="protocol-card">
            <div><div class="plabel">Protocolo</div><div class="pcode" id="trackCode"></div></div>
            <span class="status-badge badge-amber">🔄 Em análise</span>
          </div>
          <div class="timeline">
            <div class="timeline-item">
              <div class="timeline-left"><div class="timeline-dot done"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20,6 9,17 4,12"/></svg></div><div class="timeline-line"></div></div>
              <div class="timeline-body"><div class="timeline-title">Recebida <span class="status-badge badge-green">✓</span></div><div class="timeline-desc">Registrada com total sigilo.</div><div class="timeline-date">📅 Hoje, 10h23</div></div>
            </div>
            <div class="timeline-item">
              <div class="timeline-left"><div class="timeline-dot done"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20,6 9,17 4,12"/></svg></div><div class="timeline-line"></div></div>
              <div class="timeline-body"><div class="timeline-title">Triagem <span class="status-badge badge-green">✓</span></div><div class="timeline-desc">Tipo de ocorrência classificado.</div><div class="timeline-date">📅 Hoje, 10h45</div></div>
            </div>
            <div class="timeline-item">
              <div class="timeline-left"><div class="timeline-dot active"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12,6 12,12 16,14"/></svg></div><div class="timeline-line"></div></div>
              <div class="timeline-body"><div class="timeline-title">Em análise <span class="status-badge badge-amber">🔄</span></div><div class="timeline-desc">Prazo estimado: 48 horas úteis.</div><div class="timeline-date">📅 Previsão: amanhã</div></div>
            </div>
            <div class="timeline-item">
              <div class="timeline-left"><div class="timeline-dot pending"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/></svg></div><div class="timeline-line"></div></div>
              <div class="timeline-body"><div class="timeline-title">Encaminhamento <span class="status-badge badge-gray">⏳</span></div><div class="timeline-desc">Encaminhada aos órgãos competentes.</div><div class="timeline-date">📅 Em breve</div></div>
            </div>
            <div class="timeline-item">
              <div class="timeline-left"><div class="timeline-dot pending"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/></svg></div></div>
              <div class="timeline-body"><div class="timeline-title">Resolução <span class="status-badge badge-gray">⏳</span></div><div class="timeline-desc">Conclusão e retorno sobre medidas.</div><div class="timeline-date">📅 Em breve</div></div>
            </div>
          </div>
        </div>
        <div id="noResult" style="display:none;text-align:center;padding:20px 0;">
          <div style="font-size:36px;margin-bottom:10px;">🔍</div>
          <div style="font-size:14px;font-weight:600;margin-bottom:4px;">Protocolo não encontrado</div>
          <div style="font-size:13px;color:var(--text-muted);">Verifique o número e tente novamente.</div>
        </div>
      </div>

      <!-- DIREITOS -->
      <div class="section-title">⚖️ Seus direitos</div>
      <div class="right-item">
        <div class="right-icon">⚖️</div>
        <div class="right-body"><h3>Lei Maria da Penha</h3><p>Proteção do Estado, medidas protetivas de urgência solicitáveis em qualquer horário.</p><div class="right-law">📜 Lei nº 11.340/2006</div></div>
      </div>
      <div class="right-item">
        <div class="right-icon">🏥</div>
        <div class="right-body"><h3>Atendimento médico gratuito</h3><p>Coleta de vestígios e anticoncepcionais de emergência pelo SUS após violência sexual.</p><div class="right-law">📜 Lei nº 12.845/2013</div></div>
      </div>
      <div class="right-item">
        <div class="right-icon">🛡️</div>
        <div class="right-body"><h3>Medida protetiva de urgência</h3><p>Afastamento do agressor do lar, proibição de contato, decisão judicial em 48h.</p><div class="right-law">📜 Art. 22 da Lei Maria da Penha</div></div>
      </div>
      <div class="right-item">
        <div class="right-icon">🏠</div>
        <div class="right-body"><h3>Direito à moradia segura</h3><p>Acolhimento em casa abrigo sigilosa com filhos menores durante situação de risco.</p><div class="right-law">📜 Art. 9º da Lei Maria da Penha</div></div>
      </div>
      <div class="right-item">
        <div class="right-icon">💼</div>
        <div class="right-body"><h3>Proteção no emprego</h3><p>Suspensão do contrato de trabalho por até 6 meses sem perder o emprego.</p><div class="right-law">📜 Art. 9º, §2º da Lei Maria da Penha</div></div>
      </div>
      <div class="right-item">
        <div class="right-icon">🔒</div>
        <div class="right-body"><h3>Direito ao sigilo</h3><p>Dados pessoais não divulgados. Nenhum meio pode revelar seu nome ou localização.</p><div class="right-law">📜 Art. 12 da Lei Maria da Penha</div></div>
      </div>

      <div class="section-gap"></div>

      <!-- FAQ -->
      <div class="section-title">❓ Perguntas frequentes</div>
      <div class="faq-item"><button class="faq-question" onclick="toggleFaq(this)">O que é a Lei Maria da Penha?<svg class="faq-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6,9 12,15 18,9"/></svg></button><div class="faq-answer">É a Lei nº 11.340/2006 que cria mecanismos para coibir a violência doméstica contra a mulher, com medidas protetivas e penas mais rigorosas.</div></div>
      <div class="faq-item"><button class="faq-question" onclick="toggleFaq(this)">Posso denunciar sem revelar minha identidade?<svg class="faq-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6,9 12,15 18,9"/></svg></button><div class="faq-answer">Sim! Pelo 181 (Disque-Denúncia), pelo chat ou formulário com modo anônimo ativado. A Central 180 também garante sigilo total.</div></div>
      <div class="faq-item"><button class="faq-question" onclick="toggleFaq(this)">O que acontece após minha denúncia?<svg class="faq-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6,9 12,15 18,9"/></svg></button><div class="faq-answer">Nossa equipe faz triagem e encaminha aos órgãos competentes. Você recebe protocolo para acompanhar. Casos urgentes são priorizados.</div></div>
      <div class="faq-item"><button class="faq-question" onclick="toggleFaq(this)">Posso denunciar violência sofrida por outra pessoa?<svg class="faq-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6,9 12,15 18,9"/></svg></button><div class="faq-answer">Sim! Qualquer pessoa pode denunciar. Em muitos casos a vítima tem medo de se manifestar, por isso denúncias de terceiros são muito importantes.</div></div>
      <div class="faq-item"><button class="faq-question" onclick="toggleFaq(this)">Preciso de provas para denunciar?<svg class="faq-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6,9 12,15 18,9"/></svg></button><div class="faq-answer">Não. Seu depoimento já é prova. Fotos, mensagens e áudios fortalecem o caso, mas não são obrigatórios para registrar a denúncia.</div></div>
      <div class="faq-item"><button class="faq-question" onclick="toggleFaq(this)">Violência psicológica é crime?<svg class="faq-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6,9 12,15 18,9"/></svg></button><div class="faq-answer">Sim! Tipificada no Art. 147-B do Código Penal, com pena de 6 meses a 2 anos. Ameaças, humilhações e manipulação são crime.</div></div>

      <div class="section-gap"></div>

      <!-- QUIZ -->
      <div class="section-title">📚 Teste seus conhecimentos</div>
      <div class="card">
        <div id="quizContainer">
          <div class="quiz-step active" id="qstep-0">
            <div class="quiz-q">1. O Ligue 180 funciona em qual horário?</div>
            <div class="quiz-options">
              <button class="quiz-opt" onclick="responder(this,false,'O Ligue 180 funciona 24h por dia, 7 dias por semana, inclusive feriados.')">Seg a Sex, 8h às 18h</button>
              <button class="quiz-opt" onclick="responder(this,false,'O Ligue 180 funciona 24h por dia, 7 dias por semana, inclusive feriados.')">Seg a Dom, 8h às 22h</button>
              <button class="quiz-opt" onclick="responder(this,true,'Correto! 24h por dia, todos os dias do ano, incluindo feriados. Gratuito.')">24h por dia, 7 dias por semana</button>
              <button class="quiz-opt" onclick="responder(this,false,'O Ligue 180 funciona 24h por dia, 7 dias por semana, inclusive feriados.')">Apenas dias úteis</button>
            </div>
            <div class="quiz-feedback" id="qfb-0"></div>
          </div>
          <div class="quiz-step" id="qstep-1">
            <div class="quiz-q">2. Violência psicológica é crime no Brasil?</div>
            <div class="quiz-options">
              <button class="quiz-opt" onclick="responder(this,true,'Sim! Art. 147-B do Código Penal. Pena de 6 meses a 2 anos.')">Sim, previsto no Código Penal</button>
              <button class="quiz-opt" onclick="responder(this,false,'Errado. É crime desde 2021, com pena de até 2 anos.')">Não, só física é crime</button>
              <button class="quiz-opt" onclick="responder(this,false,'Errado. É crime e pode ser denunciada.')">Só com testemunhas</button>
              <button class="quiz-opt" onclick="responder(this,false,'Errado. Não precisa de laudo.')">Só com laudo médico</button>
            </div>
            <div class="quiz-feedback" id="qfb-1"></div>
          </div>
          <div class="quiz-step" id="qstep-2">
            <div class="quiz-q">3. Para pedir medida protetiva, preciso de:</div>
            <div class="quiz-options">
              <button class="quiz-opt" onclick="responder(this,false,'Você não precisa de advogado.')">Advogado particular</button>
              <button class="quiz-opt" onclick="responder(this,false,'Não é necessário ter fotos.')">Fotos como prova</button>
              <button class="quiz-opt" onclick="responder(this,true,'Correto! Só ir à delegacia, registrar B.O. e pedir. O juiz decide em 48h.')">Apenas ir à delegacia e fazer B.O.</button>
              <button class="quiz-opt" onclick="responder(this,false,'Não precisa de autorização prévia.')">Autorização prévia do juiz</button>
            </div>
            <div class="quiz-feedback" id="qfb-2"></div>
          </div>
          <div class="quiz-step" id="qstep-result">
            <div class="quiz-result">
              <div class="trophy">🏆</div>
              <div class="score" id="quizScore">0/3</div>
              <h3 id="quizMsg" style="font-size:17px;margin-bottom:8px;"></h3>
              <p id="quizSubMsg" style="font-size:13px;color:var(--text-muted);line-height:1.6;"></p>
              <button class="btn-primary" style="margin-top:20px;" onclick="resetQuiz()">Refazer o quiz</button>
            </div>
          </div>
        </div>
        <div class="quiz-nav" id="quizNav">
          <div class="quiz-progress">Pergunta <span id="qNum">1</span> de 3</div>
          <button class="btn-secondary" id="nextBtn" onclick="nextQuestion()" disabled>Próxima →</button>
        </div>
      </div>
    </div>

  </div><!-- /pages -->

  <!-- BOTTOM NAV -->
  <nav class="bottom-nav">
    <button class="nav-item active" id="nav-inicio" onclick="goPage('inicio','nav-inicio')">
      <div class="nav-icon">🏠</div>
      <div class="nav-label">Início</div>
    </button>
    <button class="nav-item" id="nav-denuncia" onclick="goPage('denuncia','nav-denuncia')">
      <div class="nav-icon">📝</div>
      <div class="nav-label">Denúncia</div>
    </button>
    <button class="nav-item" id="nav-apoio" onclick="goPage('apoio','nav-apoio')">
      <div class="nav-icon">💜</div>
      <div class="nav-label">Apoio</div>
    </button>
    <button class="nav-item" id="nav-contato" onclick="goPage('contato','nav-contato')">
      <div class="nav-icon">📞</div>
      <div class="nav-label">Contato</div>
    </button>
    <button class="nav-item" id="nav-mais" onclick="goPage('mais','nav-mais')">
      <div class="nav-icon">☰</div>
      <div class="nav-label">Mais</div>
    </button>
  </nav>

</div><!-- /app -->

<!-- SUCCESS OVERLAY -->
<div class="success-overlay" id="successOverlay" onclick="closeSuccess(event)">
  <div class="success-card">
    <div class="success-icon">💜</div>
    <h2>Denúncia enviada!</h2>
    <p>Registramos com segurança. Nossa equipe analisará com total sigilo.</p>
    <div class="success-code">Protocolo: #AV-<span id="protocol"></span></div>
    <p style="font-size:12px;">Guarde este número para acompanhar em "Mais → Acompanhar".</p>
    <button class="btn-close" onclick="closeSuccess()">Fechar</button>
  </div>
</div>

<script>
// NAVEGAÇÃO
function goPage(pageId, navId) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('page-' + pageId).classList.add('active');
  if (navId) document.getElementById(navId).classList.add('active');
  document.getElementById('pages').scrollTo(0, 0);
}

// TIPO DENÚNCIA
function selectType(btn) {
  document.querySelectorAll('.type-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
}

// ENVIO FORM
function submitForm() {
  const code = Math.floor(100000 + Math.random() * 900000);
  document.getElementById('protocol').textContent = code;
  document.getElementById('successOverlay').classList.add('show');
}
function closeSuccess(e) {
  if (!e || e.target === document.getElementById('successOverlay'))
    document.getElementById('successOverlay').classList.remove('show');
}

// CHAT
const respostas = [
  'Obrigada por compartilhar. 💜 Você está sendo muito corajosa. Pode me contar mais, se sentir confortável?',
  'Entendo. Saiba que tudo que me disser é completamente sigiloso. Estamos aqui para te apoiar.',
  'Sua segurança é nossa prioridade. Posso te orientar sobre como registrar uma denúncia formal. Deseja continuar pelo chat ou pelo formulário?',
  'Vou registrar o que você me contou. Nossa equipe especializada entrará em contato pelo canal que preferir. Você pode ligar para o 180 a qualquer momento — gratuito, 24h.',
  'Estamos aqui sempre que precisar. 💜 O mais importante é que você está segura agora.',
];
let chatCount = 0;
function sendChat() {
  const input = document.getElementById('chatInput');
  const msg = input.value.trim();
  if (!msg) return;
  const msgs = document.getElementById('chatMessages');
  const u = document.createElement('div');
  u.className = 'msg user';
  u.innerHTML = `<div class="msg-bubble">${msg}</div><div class="msg-time">Agora</div>`;
  msgs.appendChild(u);
  input.value = '';
  input.style.height = 'auto';
  msgs.scrollTop = msgs.scrollHeight;
  setTimeout(() => {
    const b = document.createElement('div');
    b.className = 'msg bot';
    b.innerHTML = `<div class="msg-bubble">${respostas[chatCount % respostas.length]}</div><div class="msg-time">Agora</div>`;
    msgs.appendChild(b);
    msgs.scrollTop = msgs.scrollHeight;
    chatCount++;
  }, 900);
}
function chatKeyDown(e) {
  if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendChat(); }
}
function autoResize(el) {
  el.style.height = 'auto';
  el.style.height = Math.min(el.scrollHeight, 100) + 'px';
}

// PROTOCOLO
function buscarProtocolo() {
  const val = document.getElementById('protocolInput').value.trim();
  document.getElementById('trackingResult').style.display = 'none';
  document.getElementById('noResult').style.display = 'none';
  if (!val) return;
  if (val.toUpperCase().startsWith('AV-') && val.length >= 9) {
    document.getElementById('trackCode').textContent = val.toUpperCase();
    document.getElementById('trackingResult').style.display = 'block';
  } else {
    document.getElementById('noResult').style.display = 'block';
  }
}

// VÍDEOS
function openVideo(url, container) {
  const iframe = document.createElement('iframe');
  iframe.src = url + '?autoplay=1';
  iframe.allow = 'autoplay; encrypted-media';
  iframe.style.cssText = 'width:100%;height:100%;border:none;position:absolute;inset:0;';
  container.innerHTML = '';
  container.style.position = 'relative';
  container.appendChild(iframe);
}

// FAQ
function toggleFaq(btn) {
  const answer = btn.nextElementSibling;
  const isOpen = btn.classList.contains('open');
  document.querySelectorAll('.faq-question').forEach(q => { q.classList.remove('open'); q.nextElementSibling.classList.remove('open'); });
  if (!isOpen) { btn.classList.add('open'); answer.classList.add('open'); }
}

// QUIZ
let currentQ = 0, score = 0, answered = false;
const totalQ = 3;
function responder(btn, correct, feedback) {
  if (answered) return;
  answered = true;
  btn.classList.add(correct ? 'correct' : 'wrong');
  const fb = document.getElementById('qfb-' + currentQ);
  fb.textContent = (correct ? '✅ ' : '❌ ') + feedback;
  fb.className = 'quiz-feedback show ' + (correct ? 'correct' : 'wrong');
  if (correct) score++;
  document.getElementById('nextBtn').disabled = false;
}
function nextQuestion() {
  document.getElementById('qstep-' + currentQ).classList.remove('active');
  currentQ++;
  answered = false;
  document.getElementById('nextBtn').disabled = true;
  if (currentQ >= totalQ) {
    document.getElementById('qstep-result').classList.add('active');
    document.getElementById('quizNav').style.display = 'none';
    document.getElementById('quizScore').textContent = score + '/' + totalQ;
    const msgs = [
      ['Vamos aprender mais! 📚','Explore a seção Direitos para se proteger melhor.'],
      ['Bom começo! 👍','Continue aprendendo e compartilhe com outras mulheres.'],
      ['Parabéns! 🏆','Você conhece bem seus direitos. Isso faz diferença!'],
    ];
    const t = score === 0 ? 0 : score < totalQ ? 1 : 2;
    document.getElementById('quizMsg').textContent = msgs[t][0];
    document.getElementById('quizSubMsg').textContent = msgs[t][1];
  } else {
    document.getElementById('qstep-' + currentQ).classList.add('active');
    document.getElementById('qNum').textContent = currentQ + 1;
  }
}
function resetQuiz() {
  currentQ = 0; score = 0; answered = false;
  document.querySelectorAll('.quiz-step').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.quiz-opt').forEach(o => o.className = 'quiz-opt');
  document.querySelectorAll('.quiz-feedback').forEach(f => { f.className = 'quiz-feedback'; f.textContent = ''; });
  document.getElementById('qstep-0').classList.add('active');
  document.getElementById('quizNav').style.display = 'flex';
  document.getElementById('qNum').textContent = '1';
  document.getElementById('nextBtn').disabled = true;
}
</script>
</body>
</html>
