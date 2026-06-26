<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Coffee Universe – The Heaven for Coffee Lovers</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Inter:wght@300;400;500;600&family=Playfair+Display:wght@400;700;900&display=swap" rel="stylesheet">
<style>
:root {
  --espresso: #1a0a00;
  --dark-roast: #0d0500;
  --brew: #2c1408;
  --mahogany: #3d1a00;
  --caramel: #c8781a;
  --gold: #d4a843;
  --amber-light: #e8c472;
  --cream: #f5e6c8;
  --ivory: #faf4e8;
  --smoke: rgba(245,230,200,0.06);
  --glass: rgba(255,255,255,0.04);
  --glass-border: rgba(200,120,26,0.18);
  --text-primary: #f5e6c8;
  --text-secondary: rgba(245,230,200,0.65);
  --text-muted: rgba(245,230,200,0.35);
}
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; font-size: 16px; }
body {
  background: var(--dark-roast);
  color: var(--text-primary);
  font-family: 'Inter', sans-serif;
  overflow-x: hidden;
  cursor: default;
}
/* ── CUSTOM CURSOR ── */
.cursor-dot {
  position: fixed; width: 8px; height: 8px; background: var(--caramel);
  border-radius: 50%; pointer-events: none; z-index: 9999;
  transform: translate(-50%,-50%); transition: transform 0.1s;
}
.cursor-ring {
  position: fixed; width: 36px; height: 36px;
  border: 1.5px solid rgba(200,120,26,0.5); border-radius: 50%;
  pointer-events: none; z-index: 9998; transform: translate(-50%,-50%);
  transition: width 0.3s, height 0.3s, border-color 0.3s, transform 0.15s;
}
/* ── SCROLLBAR ── */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--dark-roast); }
::-webkit-scrollbar-thumb { background: var(--caramel); border-radius: 2px; }
/* ── PARTICLES CANVAS ── */
#particle-canvas { position: fixed; top:0; left:0; width:100%; height:100%; pointer-events:none; z-index:0; }
/* ── NAV ── */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
  padding: 1.2rem 4rem;
  display: flex; align-items: center; justify-content: space-between;
  background: linear-gradient(to bottom, rgba(13,5,0,0.95), transparent);
  backdrop-filter: blur(0px);
  transition: backdrop-filter 0.4s, background 0.4s;
}
nav.scrolled {
  backdrop-filter: blur(20px);
  background: rgba(13,5,0,0.85);
  border-bottom: 1px solid var(--glass-border);
}
.nav-logo {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.5rem; font-weight: 600; letter-spacing: 0.05em;
  color: var(--caramel); text-decoration: none;
}
.nav-logo span { color: var(--amber-light); }
.nav-links { display: flex; gap: 2.5rem; list-style: none; }
.nav-links a {
  font-size: 0.78rem; letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--text-secondary); text-decoration: none;
  transition: color 0.3s; font-weight: 500;
}
.nav-links a:hover { color: var(--caramel); }
.nav-actions { display: flex; gap: 1rem; align-items: center; }
.cart-btn {
  position: relative; background: none; border: 1.5px solid var(--glass-border);
  color: var(--text-primary); padding: 0.5rem 1.2rem; border-radius: 2rem;
  cursor: pointer; font-size: 0.78rem; letter-spacing: 0.1em; text-transform: uppercase;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
  backdrop-filter: blur(10px); background: rgba(200,120,26,0.08);
}
.cart-btn:hover { background: rgba(200,120,26,0.2); border-color: var(--caramel); }
.cart-count {
  position: absolute; top: -6px; right: -6px; width: 18px; height: 18px;
  background: var(--caramel); border-radius: 50%; font-size: 0.65rem;
  display: flex; align-items: center; justify-content: center; font-weight: 600;
  color: var(--dark-roast);
}
/* ── HERO ── */
#hero {
  position: relative; height: 100vh; display: flex; align-items: center; justify-content: center;
  text-align: center; overflow: hidden; z-index: 1;
}
.hero-bg {
  position: absolute; inset: 0;
  background: radial-gradient(ellipse 80% 60% at 50% 60%, rgba(44,20,8,0.9) 0%, var(--dark-roast) 70%);
}
.hero-coffee-ring {
  position: absolute; width: 700px; height: 700px; border-radius: 50%;
  border: 1px solid rgba(200,120,26,0.1);
  animation: spin-slow 40s linear infinite;
}
.hero-coffee-ring::before {
  content: ''; position: absolute; inset: 40px; border-radius: 50%;
  border: 1px solid rgba(200,120,26,0.06);
}
@keyframes spin-slow { to { transform: rotate(360deg); } }
.hero-content { position: relative; z-index: 2; max-width: 800px; padding: 0 2rem; }
.hero-eyebrow {
  font-size: 0.72rem; letter-spacing: 0.3em; text-transform: uppercase;
  color: var(--caramel); margin-bottom: 1.5rem; opacity: 0;
  animation: fade-up 1s 0.3s forwards;
}
.hero-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(3rem, 7vw, 6.5rem); font-weight: 900; line-height: 1.05;
  margin-bottom: 1.5rem; opacity: 0; animation: fade-up 1s 0.5s forwards;
}
.hero-title .highlight {
  background: linear-gradient(135deg, var(--caramel), var(--amber-light), var(--caramel));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  background-size: 200% 100%; animation: shimmer 4s 1.5s infinite;
}
@keyframes shimmer { 0%,100% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } }
.hero-sub {
  font-family: 'Cormorant Garamond', serif; font-size: 1.4rem;
  color: var(--text-secondary); font-style: italic; margin-bottom: 3rem;
  opacity: 0; animation: fade-up 1s 0.7s forwards;
}
.hero-btns {
  display: flex; gap: 1.2rem; justify-content: center; flex-wrap: wrap;
  opacity: 0; animation: fade-up 1s 0.9s forwards;
}
@keyframes fade-up {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
.btn-primary {
  padding: 0.9rem 2.5rem; background: var(--caramel); color: var(--dark-roast);
  border: none; border-radius: 3rem; cursor: pointer; font-size: 0.82rem;
  font-weight: 600; letter-spacing: 0.12em; text-transform: uppercase;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
  box-shadow: 0 0 40px rgba(200,120,26,0.3);
}
.btn-primary:hover { transform: translateY(-2px) scale(1.02); box-shadow: 0 0 60px rgba(200,120,26,0.5); background: var(--gold); }
.btn-outline {
  padding: 0.9rem 2.5rem; background: transparent;
  border: 1.5px solid rgba(200,120,26,0.4); color: var(--text-primary);
  border-radius: 3rem; cursor: pointer; font-size: 0.82rem;
  font-weight: 500; letter-spacing: 0.12em; text-transform: uppercase;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
  backdrop-filter: blur(10px);
}
.btn-outline:hover { border-color: var(--caramel); background: rgba(200,120,26,0.1); transform: translateY(-2px); }
.scroll-indicator {
  position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
  display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
  opacity: 0; animation: fade-up 1s 1.5s forwards; color: var(--text-muted); font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
}
.scroll-line {
  width: 1px; height: 50px;
  background: linear-gradient(to bottom, transparent, var(--caramel), transparent);
  animation: scroll-pulse 2s infinite;
}
@keyframes scroll-pulse {
  0%,100% { opacity: 0.3; transform: scaleY(1); }
  50% { opacity: 1; transform: scaleY(1.2); }
}
/* ── STEAM ANIMATION ── */
.steam-container { position: absolute; top: 0; left: 50%; transform: translateX(-50%); width: 200px; pointer-events: none; }
.steam {
  position: absolute; bottom: 0; width: 6px; border-radius: 50%;
  background: linear-gradient(to top, rgba(245,230,200,0.3), transparent);
  filter: blur(3px); animation: steam-rise 3s ease-in infinite;
}
@keyframes steam-rise {
  0% { height: 0; opacity: 0.6; transform: translateX(0) scaleX(1); }
  50% { height: 80px; opacity: 0.3; transform: translateX(10px) scaleX(1.4); }
  100% { height: 160px; opacity: 0; transform: translateX(-5px) scaleX(0.8); }
}
/* ── SECTIONS ── */
section { position: relative; z-index: 1; }
.section-header { text-align: center; margin-bottom: 4rem; }
.section-eyebrow {
  font-size: 0.7rem; letter-spacing: 0.3em; text-transform: uppercase;
  color: var(--caramel); margin-bottom: 1rem;
}
.section-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2rem, 4vw, 3.5rem); font-weight: 700; line-height: 1.1;
}
.section-title em { color: var(--caramel); font-style: italic; }
.section-sub { color: var(--text-secondary); margin-top: 1rem; font-size: 0.95rem; line-height: 1.7; max-width: 500px; margin-left: auto; margin-right: auto; }
/* ── MOOD SELECTOR ── */
#mood { padding: 5rem 4rem; background: linear-gradient(to bottom, var(--dark-roast), var(--espresso)); }
.mood-grid { display: flex; gap: 1.2rem; justify-content: center; flex-wrap: wrap; }
.mood-card {
  background: var(--glass); border: 1px solid var(--glass-border);
  border-radius: 1.5rem; padding: 2rem 1.5rem; text-align: center; cursor: pointer;
  transition: all 0.4s; min-width: 140px; backdrop-filter: blur(20px);
  position: relative; overflow: hidden;
}
.mood-card::before {
  content: ''; position: absolute; inset: 0; opacity: 0;
  transition: opacity 0.4s;
}
.mood-card.happy::before { background: radial-gradient(circle at 50% 100%, rgba(200,120,26,0.3), transparent 70%); }
.mood-card.focus::before { background: radial-gradient(circle at 50% 100%, rgba(100,150,255,0.2), transparent 70%); }
.mood-card.relax::before { background: radial-gradient(circle at 50% 100%, rgba(100,200,150,0.2), transparent 70%); }
.mood-card.energy::before { background: radial-gradient(circle at 50% 100%, rgba(255,180,50,0.3), transparent 70%); }
.mood-card:hover { transform: translateY(-8px); border-color: var(--caramel); }
.mood-card:hover::before { opacity: 1; }
.mood-card.active { border-color: var(--caramel); background: rgba(200,120,26,0.12); }
.mood-emoji { font-size: 2.5rem; margin-bottom: 0.8rem; display: block; }
.mood-label { font-size: 0.85rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--text-secondary); font-weight: 500; }
.mood-desc { font-size: 0.75rem; color: var(--text-muted); margin-top: 0.4rem; }
/* ── BRANDS ── */
#brands { padding: 6rem 4rem; }
.brands-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.5rem; max-width: 1200px; margin: 0 auto;
}
.brand-card {
  background: var(--glass); border: 1px solid var(--glass-border);
  border-radius: 1.5rem; padding: 2rem; cursor: pointer;
  transition: all 0.4s; position: relative; overflow: hidden;
  backdrop-filter: blur(20px);
}
.brand-card::after {
  content: ''; position: absolute; inset: 0;
  background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(200,120,26,0.12) 0%, transparent 60%);
  opacity: 0; transition: opacity 0.3s;
}
.brand-card:hover { transform: translateY(-6px); border-color: rgba(200,120,26,0.5); }
.brand-card:hover::after { opacity: 1; }
.brand-logo-wrap {
  width: 64px; height: 64px; border-radius: 1rem; margin-bottom: 1.2rem;
  display: flex; align-items: center; justify-content: center;
  font-size: 2rem;
  background: rgba(200,120,26,0.1); border: 1px solid rgba(200,120,26,0.2);
  transition: transform 0.4s;
}
.brand-card:hover .brand-logo-wrap { transform: scale(1.1) rotate(-3deg); }
.brand-name {
  font-family: 'Playfair Display', serif; font-size: 1.3rem; font-weight: 700;
  margin-bottom: 0.4rem;
}
.brand-origin { font-size: 0.72rem; color: var(--caramel); letter-spacing: 0.15em; text-transform: uppercase; margin-bottom: 0.8rem; }
.brand-desc { font-size: 0.85rem; color: var(--text-secondary); line-height: 1.6; }
.brand-tag {
  display: inline-block; margin-top: 1rem;
  padding: 0.25rem 0.75rem; border-radius: 2rem;
  font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase;
  background: rgba(200,120,26,0.15); color: var(--caramel); border: 1px solid rgba(200,120,26,0.25);
}
.brand-arrow {
  position: absolute; top: 1.5rem; right: 1.5rem; width: 32px; height: 32px;
  border-radius: 50%; border: 1px solid var(--glass-border);
  display: flex; align-items: center; justify-content: center;
  font-size: 0.85rem; color: var(--text-muted);
  transition: all 0.3s;
}
.brand-card:hover .brand-arrow { background: var(--caramel); color: var(--dark-roast); border-color: var(--caramel); transform: rotate(45deg); }
/* ── PRODUCT MENU ── */
#menu { padding: 6rem 4rem; background: linear-gradient(to bottom, var(--espresso), var(--brew)); display: none; }
.menu-brand-header {
  display: flex; align-items: center; gap: 1rem; margin-bottom: 3rem;
  max-width: 1200px; margin-left: auto; margin-right: auto;
}
.back-btn {
  background: none; border: 1.5px solid var(--glass-border); color: var(--text-secondary);
  padding: 0.5rem 1.2rem; border-radius: 2rem; cursor: pointer;
  font-size: 0.75rem; letter-spacing: 0.1em; text-transform: uppercase;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
}
.back-btn:hover { border-color: var(--caramel); color: var(--caramel); }
.current-brand-name { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700; }
.products-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem; max-width: 1200px; margin: 0 auto;
}
.product-card {
  background: var(--glass); border: 1px solid var(--glass-border);
  border-radius: 1.5rem; overflow: hidden; cursor: pointer;
  transition: all 0.4s; backdrop-filter: blur(20px);
}
.product-card:hover { transform: translateY(-8px) scale(1.01); border-color: rgba(200,120,26,0.5); box-shadow: 0 20px 60px rgba(0,0,0,0.4); }
.product-visual {
  height: 180px; position: relative; display: flex; align-items: center; justify-content: center;
  overflow: hidden;
  background: radial-gradient(ellipse at 50% 100%, rgba(44,20,8,0.8), rgba(13,5,0,0.9));
}
.cup-svg { transition: transform 0.5s; }
.product-card:hover .cup-svg { transform: scale(1.1) translateY(-5px); }
.steam-mini {
  position: absolute; bottom: 50%; width: 4px; border-radius: 50%;
  background: rgba(245,230,200,0.4); filter: blur(2px);
  animation: steam-rise 2.5s ease-in infinite;
}
.product-info { padding: 1.5rem; }
.product-name { font-family: 'Playfair Display', serif; font-size: 1.15rem; font-weight: 700; margin-bottom: 0.3rem; }
.product-origin { font-size: 0.72rem; color: var(--caramel); letter-spacing: 0.12em; text-transform: uppercase; margin-bottom: 0.8rem; }
.strength-bar { display: flex; gap: 4px; margin-bottom: 0.8rem; }
.strength-dot {
  width: 8px; height: 8px; border-radius: 50%;
  background: rgba(200,120,26,0.2); transition: background 0.3s;
}
.strength-dot.active { background: var(--caramel); }
.product-flavor { font-size: 0.78rem; color: var(--text-secondary); line-height: 1.5; margin-bottom: 1rem; }
.product-price { font-size: 1.1rem; font-weight: 600; color: var(--amber-light); margin-bottom: 0.8rem; }
.add-btn {
  width: 100%; padding: 0.7rem; background: rgba(200,120,26,0.15);
  border: 1px solid rgba(200,120,26,0.3); color: var(--caramel);
  border-radius: 2rem; cursor: pointer; font-size: 0.78rem;
  letter-spacing: 0.1em; text-transform: uppercase; font-weight: 500;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
}
.add-btn:hover { background: var(--caramel); color: var(--dark-roast); border-color: var(--caramel); }
/* ── CUSTOMIZER ── */
#customizer {
  position: fixed; right: 0; top: 0; bottom: 0; width: 380px; z-index: 900;
  background: rgba(13,5,0,0.96); backdrop-filter: blur(30px);
  border-left: 1px solid var(--glass-border);
  transform: translateX(100%); transition: transform 0.5s cubic-bezier(0.4,0,0.2,1);
  overflow-y: auto; padding: 2rem;
}
#customizer.open { transform: translateX(0); }
.customizer-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 2rem; }
.customizer-title { font-family: 'Playfair Display', serif; font-size: 1.4rem; font-weight: 700; }
.close-btn {
  width: 36px; height: 36px; border-radius: 50%;
  border: 1px solid var(--glass-border); background: none;
  color: var(--text-secondary); cursor: pointer; font-size: 1.1rem;
  transition: all 0.3s; display: flex; align-items: center; justify-content: center;
}
.close-btn:hover { border-color: var(--caramel); color: var(--caramel); }
.customizer-product-name { font-family: 'Cormorant Garamond', serif; font-size: 1.1rem; color: var(--caramel); font-style: italic; margin-bottom: 2rem; }
.custom-section { margin-bottom: 2rem; }
.custom-label { font-size: 0.72rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-muted); margin-bottom: 1rem; }
.size-options { display: flex; gap: 0.8rem; }
.size-btn {
  flex: 1; padding: 0.7rem; border-radius: 0.75rem; cursor: pointer;
  border: 1px solid var(--glass-border); background: none;
  color: var(--text-secondary); font-size: 0.82rem; font-weight: 500;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
}
.size-btn:hover, .size-btn.active { border-color: var(--caramel); background: rgba(200,120,26,0.15); color: var(--caramel); }
.milk-options { display: grid; grid-template-columns: 1fr 1fr; gap: 0.6rem; }
.milk-btn {
  padding: 0.6rem; border-radius: 0.6rem; cursor: pointer;
  border: 1px solid var(--glass-border); background: none;
  color: var(--text-secondary); font-size: 0.78rem;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
}
.milk-btn:hover, .milk-btn.active { border-color: var(--caramel); background: rgba(200,120,26,0.12); color: var(--caramel); }
.temp-toggle { display: flex; border: 1px solid var(--glass-border); border-radius: 2rem; overflow: hidden; }
.temp-btn {
  flex: 1; padding: 0.6rem; cursor: pointer; background: none; border: none;
  color: var(--text-secondary); font-size: 0.82rem; transition: all 0.3s; font-family: 'Inter', sans-serif;
}
.temp-btn.active { background: var(--caramel); color: var(--dark-roast); }
.sugar-slider-wrap { padding: 0.5rem 0; }
.sugar-label-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 0.8rem; }
.sugar-value { font-size: 0.9rem; color: var(--caramel); font-weight: 600; }
input[type="range"] {
  width: 100%; -webkit-appearance: none; appearance: none;
  height: 4px; border-radius: 2px; background: rgba(200,120,26,0.2); outline: none;
}
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none; width: 18px; height: 18px; border-radius: 50%;
  background: var(--caramel); cursor: pointer;
  box-shadow: 0 0 12px rgba(200,120,26,0.5);
  transition: transform 0.2s;
}
input[type="range"]::-webkit-slider-thumb:hover { transform: scale(1.2); }
.cup-preview {
  height: 160px; display: flex; align-items: center; justify-content: center;
  background: rgba(200,120,26,0.05); border-radius: 1rem;
  border: 1px solid rgba(200,120,26,0.1); margin-bottom: 1.5rem; position: relative; overflow: hidden;
}
.order-total { font-size: 1.3rem; font-weight: 600; color: var(--amber-light); margin-bottom: 1rem; }
.order-total span { font-size: 0.8rem; color: var(--text-muted); font-weight: 400; }
/* ── CART PANEL ── */
#cart-panel {
  position: fixed; right: 0; top: 0; bottom: 0; width: 380px; z-index: 950;
  background: rgba(13,5,0,0.97); backdrop-filter: blur(30px);
  border-left: 1px solid var(--glass-border);
  transform: translateX(100%); transition: transform 0.5s cubic-bezier(0.4,0,0.2,1);
  display: flex; flex-direction: column; padding: 2rem;
}
#cart-panel.open { transform: translateX(0); }
.cart-items { flex: 1; overflow-y: auto; margin: 1.5rem 0; }
.cart-item {
  display: flex; gap: 1rem; align-items: center;
  padding: 1rem; border-radius: 1rem; margin-bottom: 0.8rem;
  background: rgba(200,120,26,0.06); border: 1px solid rgba(200,120,26,0.1);
  animation: slide-in 0.3s ease;
}
@keyframes slide-in { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
.cart-item-icon { font-size: 1.8rem; }
.cart-item-info { flex: 1; }
.cart-item-name { font-size: 0.9rem; font-weight: 500; margin-bottom: 0.2rem; }
.cart-item-detail { font-size: 0.75rem; color: var(--text-muted); }
.cart-item-price { font-size: 0.95rem; color: var(--caramel); font-weight: 600; }
.remove-item { background: none; border: none; color: var(--text-muted); cursor: pointer; font-size: 1rem; transition: color 0.2s; }
.remove-item:hover { color: #e74c3c; }
.cart-footer { border-top: 1px solid var(--glass-border); padding-top: 1.5rem; }
.cart-total-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; }
.cart-total-label { font-size: 0.85rem; color: var(--text-secondary); text-transform: uppercase; letter-spacing: 0.1em; }
.cart-total-price { font-size: 1.6rem; font-weight: 700; color: var(--amber-light); font-family: 'Playfair Display', serif; }
.checkout-btn {
  width: 100%; padding: 1.1rem; background: var(--caramel); color: var(--dark-roast);
  border: none; border-radius: 2rem; cursor: pointer; font-size: 0.88rem;
  font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase;
  transition: all 0.3s; font-family: 'Inter', sans-serif;
  box-shadow: 0 0 30px rgba(200,120,26,0.3);
}
.checkout-btn:hover { background: var(--gold); box-shadow: 0 0 50px rgba(200,120,26,0.5); transform: translateY(-2px); }
/* ── AI RECOMMENDATION ── */
#ai-rec { padding: 5rem 4rem; background: linear-gradient(135deg, rgba(44,20,8,0.6), var(--espresso)); }
.ai-card {
  max-width: 700px; margin: 0 auto; text-align: center;
  background: var(--glass); border: 1px solid var(--glass-border);
  border-radius: 2rem; padding: 3rem; backdrop-filter: blur(20px);
}
.ai-badge {
  display: inline-flex; align-items: center; gap: 0.5rem;
  padding: 0.4rem 1rem; background: rgba(200,120,26,0.15);
  border: 1px solid rgba(200,120,26,0.3); border-radius: 2rem;
  font-size: 0.72rem; letter-spacing: 0.15em; text-transform: uppercase;
  color: var(--caramel); margin-bottom: 1.5rem;
}
.ai-dot { width: 6px; height: 6px; background: var(--caramel); border-radius: 50%; animation: pulse 1.5s infinite; }
@keyframes pulse { 0%,100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.5); opacity: 0.5; } }
.ai-result {
  margin-top: 2rem; padding: 1.5rem;
  background: rgba(200,120,26,0.08); border-radius: 1.2rem;
  border: 1px solid rgba(200,120,26,0.15);
  font-family: 'Cormorant Garamond', serif; font-size: 1.1rem; font-style: italic;
  color: var(--text-secondary); display: none; line-height: 1.7;
}
/* ── MEMBERSHIP ── */
#membership { padding: 5rem 4rem; }
.membership-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 1.5rem; max-width: 1000px; margin: 0 auto; }
.membership-card {
  border-radius: 1.5rem; padding: 2.5rem; text-align: center; position: relative; overflow: hidden;
  border: 1px solid;
}
.membership-card.bronze { border-color: rgba(180,120,70,0.3); background: rgba(180,120,70,0.06); }
.membership-card.silver { border-color: rgba(180,180,200,0.3); background: rgba(180,180,200,0.06); }
.membership-card.gold {
  border-color: rgba(212,168,67,0.5);
  background: linear-gradient(135deg, rgba(212,168,67,0.1), rgba(200,120,26,0.1));
}
.membership-card.gold::before {
  content: 'MOST POPULAR'; position: absolute; top: 1.5rem; right: -2rem;
  transform: rotate(45deg) translateX(1.5rem); background: var(--caramel);
  color: var(--dark-roast); font-size: 0.6rem; letter-spacing: 0.15em;
  padding: 0.3rem 2.5rem; font-weight: 700;
}
.tier-icon { font-size: 2.5rem; margin-bottom: 1rem; }
.tier-name { font-family: 'Playfair Display', serif; font-size: 1.4rem; font-weight: 700; margin-bottom: 0.5rem; }
.tier-price { font-size: 2rem; font-weight: 700; color: var(--caramel); font-family: 'Playfair Display', serif; }
.tier-price span { font-size: 0.85rem; color: var(--text-muted); font-family: 'Inter', sans-serif; font-weight: 400; }
.tier-features { list-style: none; margin: 1.5rem 0; text-align: left; }
.tier-features li { font-size: 0.85rem; color: var(--text-secondary); padding: 0.4rem 0; display: flex; gap: 0.5rem; align-items: flex-start; }
.tier-features li::before { content: '✦'; color: var(--caramel); font-size: 0.6rem; margin-top: 0.25rem; flex-shrink: 0; }
/* ── ORDER CONFIRMATION ── */
#order-confirm {
  position: fixed; inset: 0; z-index: 2000;
  background: rgba(0,0,0,0.85); display: none; align-items: center; justify-content: center;
  backdrop-filter: blur(10px);
}
#order-confirm.show { display: flex; }
.confirm-card {
  background: rgba(20,8,0,0.98); border: 1px solid rgba(200,120,26,0.3);
  border-radius: 2rem; padding: 3rem; text-align: center; max-width: 400px; width: 90%;
  animation: scale-in 0.5s cubic-bezier(0.4,0,0.2,1);
}
@keyframes scale-in { from { opacity: 0; transform: scale(0.8); } to { opacity: 1; transform: scale(1); } }
.confirm-icon { font-size: 4rem; margin-bottom: 1rem; animation: bounce 1s 0.5s both; }
@keyframes bounce { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
.confirm-title { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700; margin-bottom: 0.5rem; }
.confirm-sub { color: var(--text-secondary); font-size: 0.95rem; line-height: 1.6; margin-bottom: 2rem; }
.confirm-time { font-family: 'Cormorant Garamond', serif; font-size: 1.2rem; font-style: italic; color: var(--caramel); margin-bottom: 2rem; }
/* ── FAVORITES ── */
.fav-btn {
  position: absolute; top: 0.8rem; right: 0.8rem; width: 32px; height: 32px;
  border-radius: 50%; background: rgba(0,0,0,0.4); border: 1px solid rgba(200,120,26,0.2);
  cursor: pointer; display: flex; align-items: center; justify-content: center;
  font-size: 0.9rem; transition: all 0.3s; color: var(--text-muted);
}
.fav-btn:hover, .fav-btn.active { background: rgba(200,120,26,0.2); color: var(--caramel); border-color: var(--caramel); }
/* ── FOOTER ── */
footer {
  padding: 4rem 4rem 2rem; border-top: 1px solid var(--glass-border);
  background: var(--dark-roast);
}
.footer-grid { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 3rem; margin-bottom: 3rem; }
.footer-brand { font-family: 'Cormorant Garamond', serif; font-size: 1.3rem; font-weight: 600; color: var(--caramel); margin-bottom: 1rem; }
.footer-desc { font-size: 0.85rem; color: var(--text-muted); line-height: 1.7; }
.footer-heading { font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-muted); margin-bottom: 1rem; }
.footer-links { list-style: none; }
.footer-links li { margin-bottom: 0.6rem; }
.footer-links a { font-size: 0.85rem; color: var(--text-secondary); text-decoration: none; transition: color 0.2s; }
.footer-links a:hover { color: var(--caramel); }
.footer-bottom { display: flex; justify-content: space-between; align-items: center; padding-top: 2rem; border-top: 1px solid rgba(200,120,26,0.1); }
.footer-copy { font-size: 0.78rem; color: var(--text-muted); }
/* ── TOAST ── */
.toast {
  position: fixed; bottom: 2rem; left: 50%; transform: translateX(-50%) translateY(100px);
  background: rgba(20,8,0,0.95); border: 1px solid rgba(200,120,26,0.4);
  backdrop-filter: blur(20px); border-radius: 3rem;
  padding: 0.8rem 1.8rem; font-size: 0.85rem; color: var(--text-primary);
  z-index: 3000; transition: transform 0.4s cubic-bezier(0.4,0,0.2,1);
}
.toast.show { transform: translateX(-50%) translateY(0); }
/* ── LOADING SCREEN ── */
#loader {
  position: fixed; inset: 0; z-index: 5000;
  background: var(--dark-roast); display: flex; flex-direction: column;
  align-items: center; justify-content: center; gap: 1.5rem;
  transition: opacity 0.8s, visibility 0.8s;
}
#loader.hidden { opacity: 0; visibility: hidden; }
.loader-title {
  font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700;
  color: var(--caramel); letter-spacing: 0.05em;
}
.loader-sub { font-size: 0.78rem; letter-spacing: 0.3em; text-transform: uppercase; color: var(--text-muted); }
.loader-progress { width: 200px; height: 1px; background: rgba(200,120,26,0.2); border-radius: 1px; overflow: hidden; }
.loader-bar { height: 100%; background: linear-gradient(to right, transparent, var(--caramel), var(--amber-light)); border-radius: 1px; animation: load 2s ease forwards; width: 0; }
@keyframes load { 0% { width: 0; } 80% { width: 90%; } 100% { width: 100%; } }
/* ── THEME TOGGLE ── */
.theme-toggle {
  position: fixed; bottom: 2rem; right: 2rem; z-index: 500;
  width: 48px; height: 48px; border-radius: 50%;
  background: rgba(20,8,0,0.9); border: 1px solid var(--glass-border);
  cursor: pointer; display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem; backdrop-filter: blur(20px); transition: all 0.3s;
}
.theme-toggle:hover { border-color: var(--caramel); transform: scale(1.1); }
/* ── SOUND BTN ── */
.sound-btn {
  position: fixed; bottom: 5.5rem; right: 2rem; z-index: 500;
  width: 48px; height: 48px; border-radius: 50%;
  background: rgba(20,8,0,0.9); border: 1px solid var(--glass-border);
  cursor: pointer; display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem; backdrop-filter: blur(20px); transition: all 0.3s;
}
.sound-btn:hover { border-color: var(--caramel); transform: scale(1.1); }
/* ── PARALLAX ── */
.parallax-layer { will-change: transform; }
/* ── SCROLL REVEAL ── */
.reveal { opacity: 0; transform: translateY(40px); transition: opacity 0.8s, transform 0.8s; }
.reveal.visible { opacity: 1; transform: translateY(0); }
/* ── RESPONSIVE ── */
@media (max-width: 768px) {
  nav { padding: 1rem 1.5rem; }
  .nav-links { display: none; }
  #hero { padding: 0 1.5rem; }
  #brands, #menu, #mood, #ai-rec, #membership { padding: 4rem 1.5rem; }
  .hero-coffee-ring { width: 300px; height: 300px; }
  footer { padding: 3rem 1.5rem 1.5rem; }
  .footer-grid { grid-template-columns: 1fr 1fr; gap: 2rem; }
  #customizer, #cart-panel { width: 100%; }
}
</style>
</head>
<body>
<!-- LOADING SCREEN -->
<div id="loader">
  <div class="loader-title">☕ Coffee Universe</div>
  <div class="loader-sub">Brewing your experience…</div>
  <div class="loader-progress"><div class="loader-bar"></div></div>
</div>

<!-- CURSOR -->
<div class="cursor-dot" id="cursor-dot"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<!-- PARTICLES -->
<canvas id="particle-canvas"></canvas>

<!-- NAV -->
<nav id="navbar">
  <a href="#" class="nav-logo">Coffee <span>Universe</span></a>
  <ul class="nav-links">
    <li><a href="#brands">Brands</a></li>
    <li><a href="#mood">Mood</a></li>
    <li><a href="#ai-rec">AI Pick</a></li>
    <li><a href="#membership">Membership</a></li>
  </ul>
  <div class="nav-actions">
    <button class="cart-btn" onclick="toggleCart()">
      ✦ Cart <span class="cart-count" id="cart-count">0</span>
    </button>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-coffee-ring"></div>
  <div class="hero-content">
    <p class="hero-eyebrow">✦ Welcome to the Universe ✦</p>
    <h1 class="hero-title">
      The Heaven for<br><span class="highlight">Coffee Lovers</span>
    </h1>
    <p class="hero-sub">"Where every sip becomes a transcendent experience"</p>
    <div class="hero-btns">
      <button class="btn-primary" onclick="scrollToBrands()">Explore Brands</button>
      <button class="btn-outline" onclick="scrollToBrands()">Order Coffee</button>
    </div>
  </div>
  <div class="scroll-indicator">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- MOOD SELECTOR -->
<section id="mood">
  <div class="section-header reveal">
    <p class="section-eyebrow">✦ Curate Your Moment ✦</p>
    <h2 class="section-title">How are you <em>feeling</em> today?</h2>
    <p class="section-sub">Select your mood and let us guide you to the perfect brew.</p>
  </div>
  <div class="mood-grid reveal">
    <div class="mood-card happy" data-mood="happy" onclick="selectMood(this,'happy')">
      <span class="mood-emoji">☀️</span>
      <div class="mood-label">Happy</div>
      <div class="mood-desc">Bright & celebratory</div>
    </div>
    <div class="mood-card focus" data-mood="focus" onclick="selectMood(this,'focus')">
      <span class="mood-emoji">🎯</span>
      <div class="mood-label">Focus</div>
      <div class="mood-desc">Deep & concentrated</div>
    </div>
    <div class="mood-card relax" data-mood="relax" onclick="selectMood(this,'relax')">
      <span class="mood-emoji">🌿</span>
      <div class="mood-label">Relax</div>
      <div class="mood-desc">Smooth & unhurried</div>
    </div>
    <div class="mood-card energy" data-mood="energy" onclick="selectMood(this,'energy')">
      <span class="mood-emoji">⚡</span>
      <div class="mood-label">Energy</div>
      <div class="mood-desc">Bold & invigorating</div>
    </div>
  </div>
</section>

<!-- BRANDS -->
<section id="brands">
  <div class="section-header reveal">
    <p class="section-eyebrow">✦ The World's Finest ✦</p>
    <h2 class="section-title">Choose Your <em>Brand Universe</em></h2>
    <p class="section-sub">Each brand, a world. Each cup, a journey. Step into your universe.</p>
  </div>
  <div class="brands-grid" id="brands-grid">
  </div>
</section>

<!-- PRODUCT MENU -->
<section id="menu">
  <div class="menu-brand-header">
    <button class="back-btn" onclick="showBrands()">← Back</button>
    <h2 class="current-brand-name" id="current-brand-display"></h2>
  </div>
  <div class="products-grid" id="products-grid"></div>
</section>

<!-- AI RECOMMENDATION -->
<section id="ai-rec">
  <div class="ai-card reveal">
    <div class="ai-badge"><div class="ai-dot"></div> AI Coffee Sommelier</div>
    <h2 class="section-title" style="margin-bottom:1rem;">Your perfect <em>brew</em></h2>
    <p style="color:var(--text-secondary);font-size:0.9rem;margin-bottom:2rem;">Answer a few questions and our AI will craft your ideal cup.</p>
    <div style="display:flex;gap:0.8rem;flex-wrap:wrap;justify-content:center;margin-bottom:1.5rem;" id="ai-prefs">
      <button class="btn-outline" style="padding:0.5rem 1.2rem;font-size:0.75rem;" onclick="toggleAIPref(this,'intense')">Intense</button>
      <button class="btn-outline" style="padding:0.5rem 1.2rem;font-size:0.75rem;" onclick="toggleAIPref(this,'smooth')">Smooth</button>
      <button class="btn-outline" style="padding:0.5rem 1.2rem;font-size:0.75rem;" onclick="toggleAIPref(this,'sweet')">Sweet</button>
      <button class="btn-outline" style="padding:0.5rem 1.2rem;font-size:0.75rem;" onclick="toggleAIPref(this,'fruity')">Fruity</button>
      <button class="btn-outline" style="padding:0.5rem 1.2rem;font-size:0.75rem;" onclick="toggleAIPref(this,'nutty')">Nutty</button>
      <button class="btn-outline" style="padding:0.5rem 1.2rem;font-size:0.75rem;" onclick="toggleAIPref(this,'cold')">Cold Brew</button>
    </div>
    <button class="btn-primary" onclick="getAIRecommendation()">✦ Recommend My Coffee</button>
    <div class="ai-result" id="ai-result"></div>
  </div>
</section>

<!-- MEMBERSHIP -->
<section id="membership">
  <div class="section-header reveal">
    <p class="section-eyebrow">✦ Exclusive Access ✦</p>
    <h2 class="section-title">Join the <em>Inner Circle</em></h2>
    <p class="section-sub">Unlock premium benefits, early access to rare beans, and priority ordering.</p>
  </div>
  <div class="membership-grid reveal">
    <div class="membership-card bronze">
      <div class="tier-icon">🥉</div>
      <div class="tier-name">Connoisseur</div>
      <div class="tier-price">₹299 <span>/month</span></div>
      <ul class="tier-features">
        <li>5% off all orders</li>
        <li>Early new arrival access</li>
        <li>Monthly brew guide</li>
        <li>Member-only blends</li>
      </ul>
      <button class="btn-outline" style="width:100%;padding:0.7rem;">Get Started</button>
    </div>
    <div class="membership-card gold">
      <div class="tier-icon">👑</div>
      <div class="tier-name">Grand Barista</div>
      <div class="tier-price">₹799 <span>/month</span></div>
      <ul class="tier-features">
        <li>15% off all orders</li>
        <li>Free premium delivery</li>
        <li>Monthly mystery box</li>
        <li>AI personal sommelier</li>
        <li>Reserve collection access</li>
        <li>Exclusive tasting events</li>
      </ul>
      <button class="btn-primary" style="width:100%;">Join Now</button>
    </div>
    <div class="membership-card silver">
      <div class="tier-icon">🥈</div>
      <div class="tier-name">Aficionado</div>
      <div class="tier-price">₹499 <span>/month</span></div>
      <ul class="tier-features">
        <li>10% off all orders</li>
        <li>Priority ordering</li>
        <li>Curated brew notes</li>
        <li>Free delivery on orders ₹299+</li>
      </ul>
      <button class="btn-outline" style="width:100%;padding:0.7rem;">Get Started</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-grid">
    <div>
      <div class="footer-brand">☕ Coffee Universe</div>
      <p class="footer-desc">The world's most curated coffee marketplace. We bring together the finest brands, rare single-origins, and artisan roasters into one immersive, luxurious experience.</p>
    </div>
    <div>
      <div class="footer-heading">Explore</div>
      <ul class="footer-links">
        <li><a href="#brands">All Brands</a></li>
        <li><a href="#mood">Mood Selector</a></li>
        <li><a href="#ai-rec">AI Sommelier</a></li>
        <li><a href="#">New Arrivals</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-heading">Company</div>
      <ul class="footer-links">
        <li><a href="#">Our Story</a></li>
        <li><a href="#">Partners</a></li>
        <li><a href="#">Careers</a></li>
        <li><a href="#">Press</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-heading">Support</div>
      <ul class="footer-links">
        <li><a href="#">Help Center</a></li>
        <li><a href="#">Track Order</a></li>
        <li><a href="#">Returns</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span class="footer-copy">© 2025 Coffee Universe. All rights reserved. Crafted with passion.</span>
    <span class="footer-copy">Made for coffee lovers, by coffee lovers.</span>
  </div>
</footer>

<!-- CUSTOMIZER -->
<div id="customizer">
  <div class="customizer-header">
    <div class="customizer-title">Customize</div>
    <button class="close-btn" onclick="closeCustomizer()">✕</button>
  </div>
  <div class="customizer-product-name" id="customizer-product-name">Select a coffee</div>
  <div class="cup-preview" id="cup-preview">
    <div style="font-size:4rem;filter:drop-shadow(0 0 20px rgba(200,120,26,0.4));" id="cup-preview-icon">☕</div>
  </div>
  <div class="custom-section">
    <div class="custom-label">Cup Size</div>
    <div class="size-options">
      <button class="size-btn" onclick="selectSize(this,'S')">S<br><span style="font-size:0.65rem;color:var(--text-muted)">180ml</span></button>
      <button class="size-btn active" onclick="selectSize(this,'M')">M<br><span style="font-size:0.65rem;color:var(--text-muted)">280ml</span></button>
      <button class="size-btn" onclick="selectSize(this,'L')">L<br><span style="font-size:0.65rem;color:var(--text-muted)">400ml</span></button>
    </div>
  </div>
  <div class="custom-section">
    <div class="custom-label">Temperature</div>
    <div class="temp-toggle">
      <button class="temp-btn active" id="temp-hot" onclick="selectTemp('hot')">🔥 Hot</button>
      <button class="temp-btn" id="temp-iced" onclick="selectTemp('iced')">🧊 Iced</button>
    </div>
  </div>
  <div class="custom-section">
    <div class="custom-label">Milk Type</div>
    <div class="milk-options">
      <button class="milk-btn active" onclick="selectMilk(this,'Dairy')">🥛 Dairy</button>
      <button class="milk-btn" onclick="selectMilk(this,'Oat')">🌾 Oat</button>
      <button class="milk-btn" onclick="selectMilk(this,'Almond')">🌰 Almond</button>
      <button class="milk-btn" onclick="selectMilk(this,'Soy')">🫘 Soy</button>
    </div>
  </div>
  <div class="custom-section">
    <div class="sugar-label-row">
      <div class="custom-label" style="margin:0">Sugar Level</div>
      <div class="sugar-value" id="sugar-val">50%</div>
    </div>
    <div class="sugar-slider-wrap">
      <input type="range" min="0" max="100" value="50" id="sugar-slider" oninput="updateSugar(this.value)">
    </div>
  </div>
  <div class="custom-section">
    <div class="order-total">₹<span id="order-price">0</span> <span>total</span></div>
    <button class="btn-primary" style="width:100%" onclick="addToCart()">Add to Cart ✦</button>
  </div>
</div>

<!-- CART PANEL -->
<div id="cart-panel">
  <div class="customizer-header">
    <div class="customizer-title">Your Cart</div>
    <button class="close-btn" onclick="toggleCart()">✕</button>
  </div>
  <div class="cart-items" id="cart-items">
    <div style="text-align:center;color:var(--text-muted);padding:3rem 0;font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-style:italic;">
      Your cart is empty.<br>Start your coffee journey.
    </div>
  </div>
  <div class="cart-footer">
    <div class="cart-total-row">
      <div class="cart-total-label">Total</div>
      <div class="cart-total-price">₹<span id="cart-total">0</span></div>
    </div>
    <button class="checkout-btn" onclick="placeOrder()">Place Order ✦</button>
  </div>
</div>

<!-- ORDER CONFIRMATION -->
<div id="order-confirm">
  <div class="confirm-card">
    <div class="confirm-icon">☕</div>
    <div class="confirm-title">Order Confirmed!</div>
    <div class="confirm-sub">Your perfect brew is being crafted with love and precision.</div>
    <div class="confirm-time">Estimated delivery: 25–35 minutes</div>
    <button class="btn-primary" onclick="closeConfirmation()">Continue Shopping ✦</button>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- FLOATING BUTTONS -->
<button class="theme-toggle" onclick="toggleTheme()" title="Toggle Theme">🌙</button>
<button class="sound-btn" onclick="toggleSound()" title="Ambient Sound" id="sound-btn">🔇</button>

<script>
// ── DATA ──
const brands = [
  { id:'starbucks', name:'Starbucks', emoji:'⭐', origin:'Seattle, USA', desc:'The world\'s most iconic coffeehouse. Bold flavors, seasonal specials, and a culture of craft.', tag:'Global Icon', color:'rgba(0,112,74,0.15)' },
  { id:'nescafe', name:'Nescafé', emoji:'🔴', origin:'Vevey, Switzerland', desc:'The world\'s most beloved instant coffee. Rich, smooth, and consistently satisfying since 1938.', tag:'Classic Heritage', color:'rgba(200,30,30,0.12)' },
  { id:'bluetokai', name:'Blue Tokai', emoji:'🔵', origin:'New Delhi, India', desc:'India\'s pioneering specialty coffee roaster. Farm-to-cup single origins with unparalleled traceability.', tag:'Indian Specialty', color:'rgba(30,100,200,0.12)' },
  { id:'lavazza', name:'Lavazza', emoji:'🟡', origin:'Turin, Italy', desc:'Italian coffee royalty since 1895. Authentic espresso blends passed down through generations.', tag:'Italian Legacy', color:'rgba(200,160,30,0.12)' },
  { id:'nespresso', name:'Nespresso', emoji:'💎', origin:'Lausanne, Switzerland', desc:'The apex of precision coffee engineering. Each capsule a masterpiece of Swiss perfection.', tag:'Premium Capsules', color:'rgba(150,120,80,0.12)' },
  { id:'costa', name:'Costa Coffee', emoji:'☕', origin:'London, UK', desc:'Britain\'s finest. The Mocha Italia blend — deep, distinctive, and unmistakably crafted.', tag:'British Craft', color:'rgba(180,60,0,0.12)' },
];

const products = {
  starbucks: [
    { name:'Pike Place Roast', origin:'Medium Roast', emoji:'☕', strength:3, flavor:'Smooth, balanced — notes of cocoa and toasted nuts with a lingering finish.', price:320, icon:'☕', hot:true },
    { name:'Espresso Roast', origin:'Dark Roast', emoji:'⚫', strength:5, flavor:'Bold, smoky intensity — rich caramel sweetness with a bold, lasting finish.', price:280, icon:'🥃', hot:true },
    { name:'Cold Brew', origin:'Cold Pressed', emoji:'🧊', strength:4, flavor:'Ultra-smooth, naturally sweet — steeped 20 hours for extraordinary depth.', price:380, icon:'🥤', hot:false },
    { name:'Vanilla Latte', origin:'Espresso Blend', emoji:'🌿', strength:2, flavor:'Velvety steamed milk, rich espresso, and the warmth of Madagascar vanilla.', price:360, icon:'🍶', hot:true },
    { name:'Caramel Macchiato', origin:'Espresso Blend', emoji:'🍮', strength:3, flavor:'Layers of vanilla, espresso, and a cascade of caramel — an art in a cup.', price:390, icon:'🍯', hot:true },
  ],
  nescafe: [
    { name:'Gold Blend', origin:'Arabica & Robusta', emoji:'🥇', strength:3, flavor:'Premium freeze-dried — smooth, rich aroma with a satisfying, full-bodied cup.', price:180, icon:'☕', hot:true },
    { name:'Classic Intense', origin:'Robusta Blend', emoji:'💪', strength:5, flavor:'Deep, powerful intensity — the purist\'s choice for a true, no-compromise espresso.', price:150, icon:'⚡', hot:true },
    { name:'Iced Café', origin:'Cold Blend', emoji:'❄️', strength:2, flavor:'Bright, refreshing — specially crafted to bloom fully over ice, never bitter.', price:200, icon:'🧊', hot:false },
    { name:'Cappuccino Mix', origin:'Milk Blend', emoji:'🌸', strength:2, flavor:'Creamy, dreamy — the classic café experience in an instant.', price:160, icon:'☁️', hot:true },
  ],
  bluetokai: [
    { name:'Attikan Estate', origin:'Chikmagalur, India', emoji:'🌿', strength:4, flavor:'Complex florals, berry brightness, and a tea-like clarity — pure single origin.', price:420, icon:'🌺', hot:true },
    { name:'Bibi Plantation', origin:'Coorg, India', emoji:'🌱', strength:3, flavor:'Dark chocolate, dried fruit, and a wonderfully clean, crisp finish.', price:480, icon:'🍫', hot:true },
    { name:'Vienna Roast', origin:'Washed Process', emoji:'☕', strength:4, flavor:'Sweet, syrupy body with notes of caramel and a smoke-kissed finish.', price:390, icon:'🏔️', hot:true },
    { name:'Monsoon Malabar', origin:'Mangalore, India', emoji:'⛈️', strength:5, flavor:'Earthy, spice-forward — an ancient monsoon-weathered bean with zero acidity.', price:520, icon:'🌧️', hot:true },
  ],
  lavazza: [
    { name:'Super Crema', origin:'Arabica & Robusta', emoji:'🇮🇹', strength:4, flavor:'Hazelnut and brown sugar on the nose — thick, persistent crema, silky body.', price:340, icon:'☕', hot:true },
    { name:'Qualità Rossa', origin:'Brazil & Uganda', emoji:'❤️', strength:4, flavor:'A full, round body with dried fruit sweetness — the Italian breakfast standard.', price:290, icon:'🍷', hot:true },
    { name:'Gran Espresso', origin:'South America', emoji:'💫', strength:5, flavor:'Powerful intensity, robust character — the espresso purist\'s ultimate cup.', price:380, icon:'⚡', hot:true },
    { name:'Tierra! Organic', origin:'Colombia & Peru', emoji:'🌍', strength:3, flavor:'Fruity, floral complexity from high-altitude certified organic farms.', price:420, icon:'🌿', hot:true },
  ],
  nespresso: [
    { name:'Ristretto', origin:'South America & E. Africa', emoji:'💎', strength:10, flavor:'Ultimate intensity — volcanic, robust, smoky with an extraordinary dark crema.', price:450, icon:'⚫', hot:true },
    { name:'Livanto', origin:'Central & S. America', emoji:'🟤', strength:6, flavor:'Round and balanced — pure, natural caramelized sweetness of the finest roast.', price:380, icon:'☕', hot:true },
    { name:'Leggero', origin:'Latin America', emoji:'🌤️', strength:4, flavor:'Long, light, delicate — naturally light roasting reveals a smooth, cereal sweetness.', price:350, icon:'☁️', hot:true },
    { name:'Barista Oat Flat White', origin:'Oat Milk Blend', emoji:'🌾', strength:5, flavor:'Silky oat milk paired with an intense espresso — the modern barista\'s signature.', price:420, icon:'🍶', hot:true },
  ],
  costa: [
    { name:'Mocha Italia', origin:'Colombia & Uganda', emoji:'🦁', strength:4, flavor:'The iconic blend — dark chocolate, subtle spice, smooth molasses finish.', price:310, icon:'☕', hot:true },
    { name:'Americano', origin:'Mocha Italia Blend', emoji:'🌊', strength:3, flavor:'Bold espresso lengthened with water — pure coffee character, no compromise.', price:260, icon:'🥃', hot:true },
    { name:'Flat White', origin:'Mocha Italia', emoji:'🤍', strength:4, flavor:'Ristretto shots with silky microfoam — concentrated, smooth, velvety perfection.', price:320, icon:'🥛', hot:true },
    { name:'Cold Brew Latte', origin:'Cold Pressed', emoji:'❄️', strength:3, flavor:'12-hour cold-extracted Costa beans with oat milk — hazelnut, vanilla, chocolate.', price:370, icon:'🧊', hot:false },
  ],
};

// ── STATE ──
let cart = [];
let cartTotal = 0;
let currentProduct = null;
let selectedSize = 'M';
let selectedTemp = 'hot';
let selectedMilk = 'Dairy';
let sugarLevel = 50;
let aiPrefs = [];
let favorites = new Set();
const sizeMultiplier = { S: 0.85, M: 1, L: 1.25 };

// ── INIT ──
window.addEventListener('load', () => {
  setTimeout(() => {
    document.getElementById('loader').classList.add('hidden');
  }, 2200);
  initParticles();
  renderBrands();
  initReveal();
  initNavScroll();
  initCursor();
});

// ── CURSOR ──
function initCursor() {
  const dot = document.getElementById('cursor-dot');
  const ring = document.getElementById('cursor-ring');
  document.addEventListener('mousemove', e => {
    dot.style.left = e.clientX + 'px'; dot.style.top = e.clientY + 'px';
    ring.style.left = e.clientX + 'px'; ring.style.top = e.clientY + 'px';
  });
  document.querySelectorAll('button, a, .brand-card, .product-card, .mood-card').forEach(el => {
    el.addEventListener('mouseenter', () => { ring.style.width = '50px'; ring.style.height = '50px'; ring.style.borderColor = 'rgba(200,120,26,0.8)'; });
    el.addEventListener('mouseleave', () => { ring.style.width = '36px'; ring.style.height = '36px'; ring.style.borderColor = 'rgba(200,120,26,0.5)'; });
  });
}

// ── PARTICLES ──
function initParticles() {
  const canvas = document.getElementById('particle-canvas');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth; canvas.height = window.innerHeight;
  window.addEventListener('resize', () => { canvas.width = window.innerWidth; canvas.height = window.innerHeight; });
  const particles = [];
  const count = 60;
  const beanChars = ['●', '◉', '◎', '○', '⬤'];
  for (let i = 0; i < count; i++) {
    particles.push({
      x: Math.random() * canvas.width, y: Math.random() * canvas.height,
      vx: (Math.random() - 0.5) * 0.3, vy: -Math.random() * 0.4 - 0.1,
      size: Math.random() * 4 + 2, alpha: Math.random() * 0.15 + 0.03,
      char: beanChars[Math.floor(Math.random() * beanChars.length)],
      rot: Math.random() * Math.PI * 2, rotSpeed: (Math.random() - 0.5) * 0.01,
    });
  }
  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach(p => {
      p.x += p.vx; p.y += p.vy; p.rot += p.rotSpeed;
      if (p.y < -20) { p.y = canvas.height + 20; p.x = Math.random() * canvas.width; }
      if (p.x < -20) p.x = canvas.width + 20;
      if (p.x > canvas.width + 20) p.x = -20;
      ctx.save(); ctx.translate(p.x, p.y); ctx.rotate(p.rot);
      ctx.globalAlpha = p.alpha;
      ctx.fillStyle = `rgba(200,120,26,1)`;
      ctx.font = `${p.size * 2}px serif`;
      ctx.fillText(p.char, 0, 0);
      ctx.restore();
    });
    requestAnimationFrame(animate);
  }
  animate();
}

// ── NAV SCROLL ──
function initNavScroll() {
  window.addEventListener('scroll', () => {
    const nav = document.getElementById('navbar');
    nav.classList.toggle('scrolled', window.scrollY > 80);
  });
}

// ── REVEAL ──
function initReveal() {
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
}

// ── BRAND CARD MOUSE TRACKING ──
function initBrandTracking() {
  document.querySelectorAll('.brand-card').forEach(card => {
    card.addEventListener('mousemove', e => {
      const rect = card.getBoundingClientRect();
      const x = ((e.clientX - rect.left) / rect.width * 100).toFixed(1);
      const y = ((e.clientY - rect.top) / rect.height * 100).toFixed(1);
      card.style.setProperty('--mx', x + '%');
      card.style.setProperty('--my', y + '%');
    });
  });
}

// ── RENDER BRANDS ──
function renderBrands() {
  const grid = document.getElementById('brands-grid');
  grid.innerHTML = brands.map(b => `
    <div class="brand-card reveal" onclick="openBrand('${b.id}')" style="background:${b.color}">
      <div class="brand-arrow">→</div>
      <div class="brand-logo-wrap">${b.emoji}</div>
      <div class="brand-name">${b.name}</div>
      <div class="brand-origin">${b.origin}</div>
      <div class="brand-desc">${b.desc}</div>
      <div class="brand-tag">${b.tag}</div>
    </div>
  `).join('');
  initReveal(); initBrandTracking();
}

// ── OPEN BRAND ──
function openBrand(brandId) {
  const brand = brands.find(b => b.id === brandId);
  const productList = products[brandId];
  document.getElementById('current-brand-display').textContent = brand.emoji + '  ' + brand.name;
  const grid = document.getElementById('products-grid');
  grid.innerHTML = productList.map((p, i) => `
    <div class="product-card reveal" style="animation-delay:${i*0.08}s">
      <div class="product-visual">
        <button class="fav-btn" onclick="event.stopPropagation();toggleFav(this,'${brandId}-${i}')" id="fav-${brandId}-${i}">♡</button>
        <div class="cup-svg" style="font-size:4.5rem;filter:drop-shadow(0 0 25px rgba(200,120,26,0.35));">${p.icon}</div>
        <div class="steam-mini" style="left:50%;animation-delay:0s"></div>
        <div class="steam-mini" style="left:45%;animation-delay:0.8s"></div>
        <div class="steam-mini" style="left:55%;animation-delay:1.6s"></div>
      </div>
      <div class="product-info">
        <div class="product-name">${p.name}</div>
        <div class="product-origin">${p.origin}</div>
        <div class="strength-bar">${Array.from({length:5},(_,j)=>`<div class="strength-dot ${j<p.strength?'active':''}"></div>`).join('')}</div>
        <div class="product-flavor">${p.flavor}</div>
        <div class="product-price">₹${p.price}</div>
        <button class="add-btn" onclick="openCustomizer('${brandId}',${i})">Customize & Add ✦</button>
      </div>
    </div>
  `).join('');
  document.getElementById('brands').style.display = 'none';
  document.getElementById('menu').style.display = 'block';
  initReveal();
  document.getElementById('menu').scrollIntoView({ behavior: 'smooth' });
}

function showBrands() {
  document.getElementById('menu').style.display = 'none';
  document.getElementById('brands').style.display = 'block';
  document.getElementById('brands').scrollIntoView({ behavior: 'smooth' });
}

// ── CUSTOMIZER ──
function openCustomizer(brandId, productIndex) {
  const p = products[brandId][productIndex];
  currentProduct = { ...p, brandId, productIndex };
  document.getElementById('customizer-product-name').textContent = p.name;
  document.getElementById('cup-preview-icon').textContent = p.icon;
  updateOrderPrice();
  document.getElementById('customizer').classList.add('open');
}
function closeCustomizer() { document.getElementById('customizer').classList.remove('open'); }

function selectSize(btn, size) {
  document.querySelectorAll('.size-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active'); selectedSize = size; updateOrderPrice();
}
function selectTemp(temp) {
  selectedTemp = temp;
  document.getElementById('temp-hot').classList.toggle('active', temp === 'hot');
  document.getElementById('temp-iced').classList.toggle('active', temp === 'iced');
  document.getElementById('cup-preview-icon').textContent = temp === 'iced' ? '🥤' : (currentProduct ? currentProduct.icon : '☕');
}
function selectMilk(btn, milk) {
  document.querySelectorAll('.milk-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active'); selectedMilk = milk;
}
function updateSugar(val) {
  sugarLevel = val;
  document.getElementById('sugar-val').textContent = val + '%';
}
function updateOrderPrice() {
  if (!currentProduct) return;
  const base = currentProduct.price;
  const total = Math.round(base * sizeMultiplier[selectedSize]);
  document.getElementById('order-price').textContent = total;
}

// ── CART ──
function addToCart() {
  if (!currentProduct) return;
  const price = Math.round(currentProduct.price * sizeMultiplier[selectedSize]);
  const item = {
    id: Date.now(), name: currentProduct.name, icon: selectedTemp === 'iced' ? '🥤' : currentProduct.icon,
    detail: `${selectedSize} · ${selectedTemp === 'hot' ? 'Hot' : 'Iced'} · ${selectedMilk} · Sugar ${sugarLevel}%`,
    price,
  };
  cart.push(item); cartTotal += price;
  updateCartUI();
  closeCustomizer();
  document.getElementById('cart-count').textContent = cart.length;
  showToast(`${item.name} added to cart ✦`);
}

function updateCartUI() {
  const el = document.getElementById('cart-items');
  if (cart.length === 0) {
    el.innerHTML = `<div style="text-align:center;color:var(--text-muted);padding:3rem 0;font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-style:italic;">Your cart is empty.<br>Start your coffee journey.</div>`;
    document.getElementById('cart-total').textContent = '0';
    return;
  }
  el.innerHTML = cart.map(item => `
    <div class="cart-item">
      <div class="cart-item-icon">${item.icon}</div>
      <div class="cart-item-info">
        <div class="cart-item-name">${item.name}</div>
        <div class="cart-item-detail">${item.detail}</div>
      </div>
      <div class="cart-item-price">₹${item.price}</div>
      <button class="remove-item" onclick="removeItem(${item.id})">✕</button>
    </div>
  `).join('');
  document.getElementById('cart-total').textContent = cartTotal;
}

function removeItem(id) {
  const idx = cart.findIndex(i => i.id === id);
  if (idx > -1) { cartTotal -= cart[idx].price; cart.splice(idx, 1); }
  document.getElementById('cart-count').textContent = cart.length;
  updateCartUI();
}

function toggleCart() {
  document.getElementById('cart-panel').classList.toggle('open');
  document.getElementById('customizer').classList.remove('open');
}

// ── ORDER ──
function placeOrder() {
  if (cart.length === 0) { showToast('Add some coffee first! ☕'); return; }
  document.getElementById('cart-panel').classList.remove('open');
  document.getElementById('order-confirm').classList.add('show');
}
function closeConfirmation() {
  cart = []; cartTotal = 0;
  document.getElementById('cart-count').textContent = '0';
  updateCartUI();
  document.getElementById('order-confirm').classList.remove('show');
  showToast('Thank you! Your coffee is on its way ☕');
}

// ── FAVORITES ──
function toggleFav(btn, id) {
  if (favorites.has(id)) { favorites.delete(id); btn.textContent = '♡'; btn.classList.remove('active'); showToast('Removed from favorites'); }
  else { favorites.add(id); btn.textContent = '♥'; btn.classList.add('active'); showToast('Added to favorites ♥'); }
}

// ── MOOD ──
function selectMood(card, mood) {
  document.querySelectorAll('.mood-card').forEach(c => c.classList.remove('active'));
  card.classList.add('active');
  const moodMap = { happy: 'Vanilla Latte or Caramel Macchiato', focus: 'Espresso or Americano', relax: 'Flat White or Latte', energy: 'Ristretto or Cold Brew' };
  showToast(`${mood.charAt(0).toUpperCase()+mood.slice(1)} mood → try a ${moodMap[mood]} ✦`);
}

// ── AI RECOMMENDATION ──
function toggleAIPref(btn, pref) {
  if (aiPrefs.includes(pref)) { aiPrefs = aiPrefs.filter(p => p !== pref); btn.style.background = 'transparent'; btn.style.color = 'var(--text-primary)'; }
  else { aiPrefs.push(pref); btn.style.background = 'rgba(200,120,26,0.2)'; btn.style.color = 'var(--caramel)'; btn.style.borderColor = 'var(--caramel)'; }
}

function getAIRecommendation() {
  const resultEl = document.getElementById('ai-result');
  resultEl.style.display = 'block';
  resultEl.textContent = '✦ Analyzing your palate preferences…';
  const recs = {
    intense: 'a Nespresso Ristretto — volcanic intensity, extraordinary dark crema, and a finish that lingers like a perfect memory.',
    smooth: 'a Blue Tokai Attikan Estate — floral clarity, berry brightness, and a tea-like cleanliness that\'s genuinely rare.',
    sweet: 'a Starbucks Caramel Macchiato — layers of vanilla, espresso, and cascading caramel — an art piece in a cup.',
    fruity: 'a Blue Tokai Bibi Plantation — dark chocolate and dried fruit complexity from the misty hills of Coorg.',
    nutty: 'a Lavazza Super Crema — hazelnut and brown sugar on the nose with a silky, persistent crema.',
    cold: 'a Starbucks Cold Brew — ultra-smooth, naturally sweet, steeped 20 hours for extraordinary depth without bitterness.',
  };
  const primary = aiPrefs.length > 0 ? aiPrefs[0] : 'smooth';
  setTimeout(() => {
    const rec = recs[primary] || recs.smooth;
    resultEl.innerHTML = `<strong style="color:var(--caramel);font-style:normal">Based on your taste profile,</strong> we recommend ${rec}`;
  }, 1200);
}

// ── SCROLL HELPERS ──
function scrollToBrands() { document.getElementById('brands').scrollIntoView({ behavior: 'smooth' }); }

// ── TOAST ──
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2800);
}

// ── THEME ──
let isDark = true;
function toggleTheme() {
  isDark = !isDark;
  document.querySelector('.theme-toggle').textContent = isDark ? '🌙' : '☀️';
  document.body.style.filter = isDark ? 'none' : 'brightness(1.1) contrast(0.95)';
}

// ── SOUND ──
let soundOn = false;
let audioCtx = null;
function toggleSound() {
  soundOn = !soundOn;
  document.getElementById('sound-btn').textContent = soundOn ? '🔊' : '🔇';
  if (soundOn) { playAmbient(); showToast('Café ambience on ♪'); }
  else { stopAmbient(); showToast('Sound off'); }
}
let gainNode;
function playAmbient() {
  audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  gainNode = audioCtx.createGain(); gainNode.gain.value = 0.03; gainNode.connect(audioCtx.destination);
  function playNoise() {
    if (!soundOn) return;
    const bufferSize = audioCtx.sampleRate * 2;
    const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
    const data = buffer.getChannelData(0);
    for (let i = 0; i < bufferSize; i++) data[i] = Math.random() * 2 - 1;
    const source = audioCtx.createBufferSource();
    source.buffer = buffer;
    const filter = audioCtx.createBiquadFilter(); filter.type = 'lowpass'; filter.frequency.value = 400;
    source.connect(filter); filter.connect(gainNode);
    source.start(); source.onended = playNoise;
  }
  playNoise();
}
function stopAmbient() { if (audioCtx) { audioCtx.close(); audioCtx = null; } }
</script>
</body>
</html>
