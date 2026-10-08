# truck-sim-hu<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TRUCK SIM HUB — Мир Симуляторов Грузовиков</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/orbitron@5.0.0/index.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/rajdhani@5.0.0/index.css">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  
  :root {
    --primary: #ff6b1a;
    --primary-glow: #ff8c42;
    --secondary: #00d4ff;
    --steam: #1b2838;
    --steam-light: #2a475e;
    --dark: #0a0e1a;
    --darker: #05070d;
    --card: #111827;
    --text: #e5e7eb;
    --muted: #9ca3af;
  }
  
  html { scroll-behavior: smooth; }
  
  body {
    font-family: 'Rajdhani', sans-serif;
    background: var(--darker);
    color: var(--text);
    overflow-x: hidden;
    line-height: 1.6;
  }
  
  h1, h2, h3, .logo, .nav-link, .btn {
    font-family: 'Orbitron', sans-serif;
    letter-spacing: 1px;
  }
  
  .bg-grid {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background-image: 
      linear-gradient(rgba(255,107,26,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,107,26,0.03) 1px, transparent 1px);
    background-size: 50px 50px;
    z-index: 0;
    pointer-events: none;
  }
  
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    background: rgba(5, 7, 13, 0.85);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(255,107,26,0.2);
    padding: 1rem 2rem;
    transition: all 0.3s;
  }
  
  .nav-container {
    max-width: 1400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
  }
  
  .logo {
    font-size: 1.5rem;
    font-weight: 900;
    background: linear-gradient(135deg, var(--primary), var(--primary-glow));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  
  .logo-icon {
    width: 40px;
    height: 40px;
    background: linear-gradient(135deg, var(--primary), #ff3d00);
    clip-path: polygon(10% 30%, 70% 30%, 75% 50%, 95% 50%, 95% 80%, 10% 80%);
    box-shadow: 0 0 20px rgba(255,107,26,0.6);
  }
  
  .nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
  }
  
  .nav-link {
    color: var(--text);
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 600;
    text-transform: uppercase;
    position: relative;
    transition: color 0.3s;
    cursor: pointer;
  }
  
  .nav-link:hover { color: var(--primary); }
  
  .nav-link::after {
    content: '';
    position: absolute;
    bottom: -5px; left: 0;
    width: 0; height: 2px;
    background: var(--primary);
    transition: width 0.3s;
  }
  
  .nav-link:hover::after { width: 100%; }
  
  .btn {
    padding: 0.7rem 1.5rem;
    background: linear-gradient(135deg, var(--primary), #ff3d00);
    color: white;
    border: none;
    border-radius: 4px;
    font-weight: 700;
    cursor: pointer;
    text-transform: uppercase;
    font-size: 0.85rem;
    transition: all 0.3s;
    box-shadow: 0 0 20px rgba(255,107,26,0.4);
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    white-space: nowrap;
  }
  
  .btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 30px rgba(255,107,26,0.8);
  }
  
  .btn-steam {
    background: linear-gradient(135deg, #1b2838, #2a475e);
    box-shadow: 0 0 20px rgba(102,192,244,0.3);
    border: 1px solid rgba(102,192,244,0.4);
  }
  
  .btn-steam:hover {
    background: linear-gradient(135deg, #2a475e, #66c0f4);
    box-shadow: 0 0 30px rgba(102,192,244,0.6);
  }
  
  .btn-outline {
    background: transparent;
    border: 2px solid var(--primary);
    box-shadow: none;
  }
  
  .btn-outline:hover {
    background: var(--primary);
    box-shadow: 0 0 20px rgba(255,107,26,0.6);
  }
  
  .icon-svg {
    width: 18px;
    height: 18px;
    display: inline-block;
    vertical-align: middle;
    flex-shrink: 0;
  }
  
  .hero {
    min-height: 100vh;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    padding: 6rem 2rem 2rem;
  }
  
  .hero-bg {
    position: absolute;
    inset: 0;
    background: 
      radial-gradient(ellipse at 20% 50%, rgba(255,107,26,0.15) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 30%, rgba(0,212,255,0.1) 0%, transparent 50%),
      linear-gradient(180deg, var(--darker) 0%, var(--dark) 100%);
    z-index: 0;
  }
  
  .hero-truck {
    position: absolute;
    bottom: 0;
    right: -5%;
    width: 70%;
    max-width: 900px;
    opacity: 0.25;
    z-index: 1;
    animation: truckFloat 6s ease-in-out infinite;
    pointer-events: none;
  }
  
  @keyframes truckFloat {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
  }
  
  .hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    max-width: 1000px;
  }
  
  .hero-badge {
    display: inline-block;
    padding: 0.5rem 1.5rem;
    background: rgba(255,107,26,0.1);
    border: 1px solid rgba(255,107,26,0.4);
    border-radius: 50px;
    color: var(--primary);
    font-size: 0.85rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 2rem;
    animation: pulse 2s infinite;
  }
  
  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 0 0 rgba(255,107,26,0.4); }
    50% { box-shadow: 0 0 0 15px rgba(255,107,26,0); }
  }
  
  .hero h1 {
    font-size: clamp(2.5rem, 7vw, 6rem);
    font-weight: 900;
    line-height: 1;
    margin-bottom: 1.5rem;
    text-transform: uppercase;
  }
  
  .hero h1 .gradient {
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-glow) 50%, #ffcc00 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    filter: drop-shadow(0 0 30px rgba(255,107,26,0.5));
  }
  
  .hero-subtitle {
    font-size: clamp(1rem, 2vw, 1.3rem);
    color: var(--muted);
    max-width: 700px;
    margin: 0 auto 2.5rem;
    font-weight: 500;
  }
  
  .hero-buttons {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }
  
  .hero-stats {
    display: flex;
    gap: 3rem;
    justify-content: center;
    margin-top: 4rem;
    flex-wrap: wrap;
  }
  
  .stat { text-align: center; }
  
  .stat-num {
    font-family: 'Orbitron', sans-serif;
    font-size: 2.5rem;
    font-weight: 900;
    color: var(--primary);
    text-shadow: 0 0 20px rgba(255,107,26,0.5);
  }
  
  .stat-label {
    color: var(--muted);
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  
  section {
    position: relative;
    z-index: 2;
    padding: 6rem 2rem;
  }
  
  .container { max-width: 1400px; margin: 0 auto; }
  
  .section-header {
    text-align: center;
    margin-bottom: 4rem;
  }
  
  .section-tag {
    color: var(--primary);
    font-size: 0.9rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 3px;
    margin-bottom: 1rem;
    display: block;
  }
  
  .section-title {
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 900;
    text-transform: uppercase;
    line-height: 1.1;
    margin-bottom: 1rem;
  }
  
  .section-title span {
    background: linear-gradient(135deg, var(--primary), var(--primary-glow));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  
  .section-desc {
    color: var(--muted);
    max-width: 600px;
    margin: 0 auto;
    font-size: 1.1rem;
  }
  
  .games-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }
  
  .game-card {
    background: var(--card);
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    transition: all 0.4s;
    border: 1px solid rgba(255,255,255,0.05);
    display: flex;
    flex-direction: column;
  }
  
  .game-card:hover {
    transform: translateY(-10px);
    border-color: var(--primary);
    box-shadow: 0 20px 60px rgba(255,107,26,0.3);
  }
  
  .game-cover {
    height: 220px;
    position: relative;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }
  
  .game-cover svg.scene {
    width: 100%;
    height: 100%;
    display: block;
  }
  
  .game-cover::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(180deg, transparent 50%, rgba(17,24,39,0.95) 100%);
    pointer-events: none;
  }
  
  .game-badge {
    position: absolute;
    top: 1rem;
    right: 1rem;
    padding: 0.3rem 0.8rem;
    background: var(--primary);
    color: white;
    font-size: 0.7rem;
    font-weight: 700;
    text-transform: uppercase;
    border-radius: 3px;
    z-index: 3;
    letter-spacing: 1px;
    pointer-events: none;
  }
  
  .steam-overlay {
    position: absolute;
    top: 1rem;
    left: 1rem;
    padding: 0.4rem 0.8rem;
    background: rgba(27,40,56,0.9);
    backdrop-filter: blur(10px);
    color: #66c0f4;
    font-size: 0.7rem;
    font-weight: 700;
    text-transform: uppercase;
    border-radius: 3px;
    z-index: 3;
    display: flex;
    align-items: center;
    gap: 0.4rem;
    border: 1px solid rgba(102,192,244,0.3);
    pointer-events: none;
  }
  
  .steam-overlay .icon-svg {
    width: 14px;
    height: 14px;
  }
  
  .game-info { 
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
  }
  
  .game-title {
    font-size: 1.3rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    text-transform: uppercase;
  }
  
  .game-meta {
    display: flex;
    gap: 1rem;
    margin-bottom: 1rem;
    font-size: 0.85rem;
    color: var(--muted);
    flex-wrap: wrap;
  }
  
  .game-meta span {
    display: flex;
    align-items: center;
    gap: 0.3rem;
  }
  
  .game-desc {
    color: var(--muted);
    font-size: 0.95rem;
    margin-bottom: 1.5rem;
    line-height: 1.5;
    flex-grow: 1;
  }
  
  .game-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 1rem;
    border-top: 1px solid rgba(255,255,255,0.05);
    gap: 1rem;
    flex-wrap: wrap;
  }
  
  .game-price-block {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
  }
  
  .game-price {
    font-family: 'Orbitron', sans-serif;
    font-size: 1.3rem;
    font-weight: 700;
    color: var(--primary);
  }
  
  .game-rating {
    display: flex;
    align-items: center;
    gap: 0.3rem;
    color: #ffcc00;
    font-weight: 700;
  }
  
  .btn-buy {
    padding: 0.6rem 1.2rem;
    background: linear-gradient(135deg, #1b2838, #2a475e);
    color: #66c0f4;
    border: 1px solid rgba(102,192,244,0.4);
    border-radius: 4px;
    font-weight: 700;
    cursor: pointer;
    text-transform: uppercase;
    font-size: 0.8rem;
    transition: all 0.3s;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    font-family: 'Orbitron', sans-serif;
    letter-spacing: 1px;
  }
  
  .btn-buy:hover {
    background: linear-gradient(135deg, #2a475e, #66c0f4);
    color: white;
    box-shadow: 0 0 20px rgba(102,192,244,0.5);
    transform: translateY(-2px);
  }
  
  .btn-buy .icon-svg {
    width: 16px;
    height: 16px;
  }
  
  .featured {
    background: linear-gradient(180deg, var(--darker) 0%, var(--dark) 100%);
  }
  
  .featured-grid {
    display: grid;
    grid-template-columns: 1.2fr 1fr;
    gap: 4rem;
    align-items: center;
  }
  
  @media (max-width: 900px) {
    .featured-grid { grid-template-columns: 1fr; }
  }
  
  .featured-visual {
    aspect-ratio: 16/10;
    border-radius: 16px;
    overflow: hidden;
    position: relative;
    border: 2px solid rgba(255,107,26,0.3);
    box-shadow: 0 30px 80px rgba(255,107,26,0.2);
  }
  
  .featured-visual svg {
    width: 100%;
    height: 100%;
    display: block;
  }
  
  .featured-tag {
    position: absolute;
    top: 1.5rem;
    left: 1.5rem;
    padding: 0.5rem 1rem;
    background: var(--primary);
    color: white;
    font-family: 'Orbitron', sans-serif;
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 2px;
    border-radius: 4px;
    z-index: 2;
    pointer-events: none;
  }
  
  .featured-content h2 {
    font-size: clamp(2rem, 4vw, 3rem);
    text-transform: uppercase;
    margin-bottom: 1rem;
    line-height: 1.1;
  }
  
  .featured-content h2 span {
    background: linear-gradient(135deg, var(--primary), var(--primary-glow));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  
  .featured-content p {
    color: var(--muted);
    margin-bottom: 2rem;
    font-size: 1.1rem;
  }
  
  .feature-list {
    list-style: none;
    margin-bottom: 2rem;
  }
  
  .feature-list li {
    padding: 0.7rem 0;
    display: flex;
    align-items: center;
    gap: 0.8rem;
    border-bottom: 1px solid rgba(255,255,255,0.05);
  }
  
  .feature-list li::before {
    content: '▶';
    color: var(--primary);
    font-size: 0.8rem;
  }
  
  .featured-buttons {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
  }
  
  .news-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
  }
  
  .news-card {
    background: var(--card);
    border-radius: 12px;
    overflow: hidden;
    transition: all 0.3s;
    border: 1px solid rgba(255,255,255,0.05);
    display: flex;
    flex-direction: column;
  }
  
  .news-card:hover {
    transform: translateY(-5px);
    border-color: rgba(255,107,26,0.3);
  }
  
  .news-image {
    height: 180px;
    position: relative;
    overflow: hidden;
    flex-shrink: 0;
  }
  
  .news-image svg {
    width: 100%;
    height: 100%;
    display: block;
  }
  
  .news-category {
    position: absolute;
    bottom: 1rem;
    left: 1rem;
    padding: 0.3rem 0.8rem;
    background: rgba(0,0,0,0.7);
    backdrop-filter: blur(10px);
    color: var(--primary);
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    border-radius: 3px;
    border: 1px solid rgba(255,107,26,0.3);
    pointer-events: none;
  }
  
  .news-content { 
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
  }
  
  .news-date {
    color: var(--muted);
    font-size: 0.8rem;
    margin-bottom: 0.5rem;
  }
  
  .news-title {
    font-size: 1.2rem;
    font-weight: 700;
    margin-bottom: 0.8rem;
    text-transform: uppercase;
    line-height: 1.3;
  }
  
  .news-excerpt {
    color: var(--muted);
    font-size: 0.9rem;
    margin-bottom: 1rem;
    flex-grow: 1;
  }
  
  .read-more {
    color: var(--primary);
    text-decoration: none;
    font-weight: 700;
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    cursor: pointer;
    transition: all 0.3s;
    align-self: flex-start;
    padding: 0.5rem 0;
  }
  
  .read-more:hover { 
    color: var(--primary-glow);
    gap: 0.7rem;
  }
  
  .community {
    background: linear-gradient(180deg, var(--dark) 0%, var(--darker) 100%);
  }
  
  .community-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
  }
  
  .community-card {
    background: linear-gradient(135deg, rgba(255,107,26,0.05), rgba(255,107,26,0.02));
    border: 1px solid rgba(255,107,26,0.15);
    border-radius: 12px;
    padding: 2rem;
    text-align: center;
    transition: all 0.3s;
    text-decoration: none;
    color: inherit;
    display: block;
    cursor: pointer;
  }
  
  .community-card:hover {
    transform: translateY(-5px);
  }
  
  .community-card.youtube:hover {
    background: linear-gradient(135deg, rgba(255,0,0,0.15), rgba(255,0,0,0.05));
    border-color: #ff0000;
  }
  
  .community-card.twitch:hover {
    background: linear-gradient(135deg, rgba(145,70,255,0.15), rgba(145,70,255,0.05));
    border-color: #9146ff;
  }
  
  .community-card.telegram:hover {
    background: linear-gradient(135deg, rgba(38,165,224,0.15), rgba(38,165,224,0.05));
    border-color: #26a5e4;
  }
  
  .community-card.lolka:hover {
    background: linear-gradient(135deg, rgba(138,43,226,0.15), rgba(138,43,226,0.05));
    border-color: #8a2be2;
  }
  
  .community-icon {
    width: 70px;
    height: 70px;
    margin: 0 auto 1rem;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s;
  }
  
  .community-icon svg {
    width: 40px;
    height: 40px;
  }
  
  .community-card.lolka .community-icon {
    background: linear-gradient(135deg, #8a2be2, #ff1493);
    box-shadow: 0 0 30px rgba(138,43,226,0.5);
  }
  
  .community-card.youtube .community-icon {
    background: linear-gradient(135deg, #ff0000, #cc0000);
    box-shadow: 0 0 30px rgba(255,0,0,0.5);
  }
  
  .community-card.twitch .community-icon {
    background: linear-gradient(135deg, #9146ff, #6441a5);
    box-shadow: 0 0 30px rgba(145,70,255,0.5);
  }
  
  .community-card.telegram .community-icon {
    background: linear-gradient(135deg, #26a5e4, #0088cc);
    box-shadow: 0 0 30px rgba(38,165,224,0.5);
  }
  
  .community-card h3 {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
    text-transform: uppercase;
  }
  
  .community-card p {
    color: var(--muted);
    font-size: 0.9rem;
    margin-bottom: 1rem;
  }
  
  .community-stat {
    font-family: 'Orbitron', sans-serif;
    font-size: 1.2rem;
    font-weight: 900;
    color: var(--primary);
  }
  
  .community-card.youtube .community-stat { color: #ff0000; }
  .community-card.twitch .community-stat { color: #9146ff; }
  .community-card.telegram .community-stat { color: #26a5e4; }
  .community-card.lolka .community-stat { color: #8a2be2; }
  
  footer {
    background: var(--darker);
    border-top: 1px solid rgba(255,107,26,0.2);
    padding: 3rem 2rem 1.5rem;
    position: relative;
    z-index: 2;
  }
  
  .footer-content {
    max-width: 1400px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 3rem;
    margin-bottom: 2rem;
  }
  
  @media (max-width: 768px) {
    .footer-content { grid-template-columns: 1fr 1fr; }
    .nav-links { display: none; }
    .nav-container { flex-wrap: wrap; }
  }
  
  .footer-col h4 {
    font-size: 1rem;
    margin-bottom: 1rem;
    text-transform: uppercase;
    color: var(--primary);
  }
  
  .footer-col ul { list-style: none; }
  .footer-col li { margin-bottom: 0.5rem; }
  
  .footer-col a {
    color: var(--muted);
    text-decoration: none;
    transition: color 0.3s;
    font-size: 0.95rem;
    cursor: pointer;
  }
  
  .footer-col a:hover { color: var(--primary); }
  
  .footer-about p {
    color: var(--muted);
    margin: 1rem 0;
    font-size: 0.95rem;
  }
  
  .social-links {
    display: flex;
    gap: 0.8rem;
    flex-wrap: wrap;
  }
  
  .social-links a {
    width: 44px;
    height: 44px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s;
    text-decoration: none;
    border: 1px solid rgba(255,255,255,0.1);
    cursor: pointer;
  }
  
  .social-links a svg {
    width: 22px;
    height: 22px;
  }
  
  .social-links a.lolka { background: rgba(138,43,226,0.15); }
  .social-links a.lolka:hover { background: #8a2be2; transform: translateY(-3px); }
  .social-links a.youtube { background: rgba(255,0,0,0.15); }
  .social-links a.youtube:hover { background: #ff0000; transform: translateY(-3px); }
  .social-links a.twitch { background: rgba(145,70,255,0.15); }
  .social-links a.twitch:hover { background: #9146ff; transform: translateY(-3px); }
  .social-links a.telegram { background: rgba(38,165,224,0.15); }
  .social-links a.telegram:hover { background: #26a5e4; transform: translateY(-3px); }
  
  .footer-bottom {
    max-width: 1400px;
    margin: 0 auto;
    padding-top: 2rem;
    border-top: 1px solid rgba(255,255,255,0.05);
    text-align: center;
    color: var(--muted);
    font-size: 0.85rem;
  }
  
  .fade-in {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s;
  }
  
  .fade-in.visible {
    opacity: 1;
    transform: translateY(0);
  }
  
  ::-webkit-scrollbar { width: 10px; }
  ::-webkit-scrollbar-track { background: var(--darker); }
  ::-webkit-scrollbar-thumb {
    background: linear-gradient(180deg, var(--primary), #ff3d00);
    border-radius: 5px;
  }
  
  .menu-toggle {
    display: none;
    background: none;
    border: none;
    color: var(--primary);
    font-size: 1.5rem;
    cursor: pointer;
  }
  
  @media (max-width: 768px) {
    .menu-toggle { display: block; }
    .hero-stats { gap: 1.5rem; }
    .stat-num { font-size: 2rem; }
  }
</style>
</head>
<body>

<div class="bg-grid"></div>

<!-- SVG DEFINITIONS -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="icon-youtube" viewBox="0 0 24 24">
      <path fill="white" d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
    </symbol>
    <symbol id="icon-twitch" viewBox="0 0 24 24">
      <path fill="white" d="M11.571 4.714h1.715v5.143H11.57zm4.715 0H18v5.143h-1.714zM6 0L1.714 4.286v15.428h5.143V24l4.286-4.286h3.428L22.286 12V0zm14.571 11.143l-3.428 3.428h-3.429l-3 3v-3H6.857V1.714h13.714Z"/>
    </symbol>
    <symbol id="icon-telegram" viewBox="0 0 24 24">
      <path fill="white" d="M11.944 0A12 12 0 0 0 0 12a12 12 0 0 0 12 12 12 12 0 0 0 12-12A12 12 0 0 0 12 0a12 12 0 0 0-.056 0zm4.962 7.224c.1-.002.321.023.465.14a.506.506 0 0 1 .171.325c.016.093.036.306.02.472-.18 1.898-.962 6.502-1.36 8.627-.168.9-.499 1.201-.82 1.23-.696.065-1.225-.46-1.9-.902-1.056-.693-1.653-1.124-2.678-1.8-1.185-.78-.417-1.21.258-1.91.177-.184 3.247-2.977 3.307-3.23.007-.032.014-.15-.056-.212s-.174-.041-.249-.024c-.106.024-1.793 1.14-5.061 3.345-.48.33-.913.49-1.302.48-.428-.008-1.252-.241-1.865-.44-.752-.245-1.349-.374-1.297-.789.027-.216.325-.437.893-.663 3.498-1.524 5.83-2.529 6.998-3.014 3.332-1.386 4.025-1.627 4.476-1.635z"/>
    </symbol>
    <symbol id="icon-steam" viewBox="0 0 24 24">
      <path fill="#66c0f4" d="M11.979 0C5.678 0 .511 4.86.022 10.965l6.432 2.658c.545-.371 1.203-.59 1.912-.59.063 0 .125.004.188.006l2.861-4.142V8.86c0-2.495 2.028-4.524 4.524-4.524 2.494 0 4.524 2.031 4.524 4.527s-2.03 4.525-4.524 4.525h-.105l-4.076 2.911c0 .052.004.105.004.159 0 1.875-1.515 3.396-3.39 3.396-1.635 0-3.016-1.173-3.331-2.727L.436 15.27C1.862 20.307 6.486 24 11.979 24c6.627 0 12-5.373 12-12S18.605 0 11.979 0zM7.54 18.21l-1.473-.61c.262.543.714.999 1.314 1.25 1.297.539 2.793-.076 3.332-1.375.263-.63.264-1.319.005-1.949s-.75-1.12-1.377-1.383c-.624-.26-1.29-.249-1.878-.03l1.523.63c.956.4 1.409 1.5 1.009 2.455-.397.957-1.497 1.41-2.454 1.012H7.54zm11.387-5.972c0-2.481-2.017-4.498-4.498-4.498-2.482 0-4.499 2.017-4.499 4.498 0 2.482 2.017 4.499 4.499 4.499 2.481 0 4.498-2.017 4.498-4.499zm-7.426.028c0-1.622 1.316-2.937 2.93-2.937 1.615 0 2.93 1.315 2.93 2.937 0 1.614-1.315 2.929-2.93 2.929-1.614 0-2.93-1.315-2.93-2.929z"/>
    </symbol>
  </defs>
</svg>

<nav>
  <div class="nav-container">
    <div class="logo">
      <div class="logo-icon"></div>
      TRUCK SIM HUB
    </div>
    <ul class="nav-links">
      <li><a href="#home" class="nav-link">Главная</a></li>
      <li><a href="#games" class="nav-link">Игры</a></li>
      <li><a href="#featured" class="nav-link">Хит</a></li>
      <li><a href="#news" class="nav-link">Новости</a></li>
      <li><a href="#community" class="nav-link">Сообщество</a></li>
    </ul>
    <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="btn btn-steam">
      <svg class="icon-svg"><use href="#icon-steam"/></svg>
      Steam
    </a>
    <button class="menu-toggle" aria-label="Меню">☰</button>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  
  <svg class="hero-truck" viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="truckGrad" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" style="stop-color:#ff6b1a"/>
        <stop offset="100%" style="stop-color:#ff3d00"/>
      </linearGradient>
    </defs>
    <rect x="50" y="150" width="450" height="150" fill="url(#truckGrad)" opacity="0.9"/>
    <rect x="60" y="160" width="430" height="130" fill="#1a1a2e" opacity="0.3"/>
    <rect x="500" y="120" width="200" height="180" fill="url(#truckGrad)"/>
    <rect x="520" y="140" width="160" height="70" fill="#00d4ff" opacity="0.6"/>
    <circle cx="150" cy="320" r="35" fill="#0a0e1a" stroke="#ff6b1a" stroke-width="3"/>
    <circle cx="250" cy="320" r="35" fill="#0a0e1a" stroke="#ff6b1a" stroke-width="3"/>
    <circle cx="600" cy="320" r="35" fill="#0a0e1a" stroke="#ff6b1a" stroke-width="3"/>
    <circle cx="680" cy="320" r="35" fill="#0a0e1a" stroke="#ff6b1a" stroke-width="3"/>
    <rect x="510" y="230" width="180" height="10" fill="#0a0e1a"/>
    <circle cx="690" cy="180" r="8" fill="#ffcc00"/>
  </svg>
  
  <div class="hero-content">
    <div class="hero-badge">⚡ Добро пожаловать в мир грузовиков</div>
    <h1>
      ПОКОРЯЙ<br>
      <span class="gradient">ДОРОГИ МИРА</span>
    </h1>
    <p class="hero-subtitle">
      Лучший портал для фанатов симуляторов грузовиков. Euro Truck Simulator 2, American Truck Simulator, SnowRunner и другие — всё в одном месте.
    </p>
    <div class="hero-buttons">
      <a href="#games" class="btn">🚛 Смотреть игры</a>
      <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="btn btn-steam">
        <svg class="icon-svg"><use href="#icon-steam"/></svg>
        Купить в Steam
      </a>
      <a href="#community" class="btn btn-outline">Вступить в клуб</a>
    </div>
    
    <div class="hero-stats">
      <div class="stat">
        <div class="stat-num">12+</div>
        <div class="stat-label">Игр в каталоге</div>
      </div>
      <div class="stat">
        <div class="stat-num">50K+</div>
        <div class="stat-label">Игроков</div>
      </div>
      <div class="stat">
        <div class="stat-num">1M+</div>
        <div class="stat-label">Километров</div>
      </div>
      <div class="stat">
        <div class="stat-num">24/7</div>
        <div class="stat-label">Онлайн</div>
      </div>
    </div>
  </div>
</section>

<!-- GAMES -->
<section id="games">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">// Каталог</span>
      <h2 class="section-title">Наши <span>Игры</span></h2>
      <p class="section-desc">Лучшие симуляторы грузовиков и внедорожной техники со всего мира</p>
    </div>
    
    <div class="games-grid">
      <!-- ETS2 -->
      <div class="game-card fade-in">
        <div class="game-cover">
          <svg class="scene" viewBox="0 0 400 220" preserveAspectRatio="xMidYMid slice">
            <defs>
              <linearGradient id="ets2bg" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#1e3a8a"/>
                <stop offset="100%" style="stop-color:#3b82f6"/>
              </linearGradient>
            </defs>
            <rect width="400" height="220" fill="url(#ets2bg)"/>
            <polygon points="0,180 80,100 160,150 240,80 320,140 400,110 400,220 0,220" fill="#1e293b" opacity="0.7"/>
            <polygon points="0,200 100,140 200,180 300,130 400,170 400,220 0,220" fill="#0f172a"/>
            <polygon points="150,220 250,220 220,140 180,140" fill="#1f2937"/>
            <rect x="170" y="145" width="60" height="40" fill="#ff6b1a"/>
            <rect x="180" y="150" width="40" height="15" fill="#00d4ff" opacity="0.6"/>
            <circle cx="185" cy="190" r="6" fill="#000"/>
            <circle cx="215" cy="190" r="6" fill="#000"/>
            <circle cx="320" cy="60" r="25" fill="#ffcc00" opacity="0.8"/>
          </svg>
          <span class="game-badge">Хит</span>
          <span class="steam-overlay"><svg class="icon-svg"><use href="#icon-steam"/></svg>Steam</span>
        </div>
        <div class="game-info">
          <h3 class="game-title">Euro Truck Simulator 2</h3>
          <div class="game-meta">
            <span>🌍 Европа</span>
            <span>🚛 Scania, Volvo, MAN</span>
          </div>
          <p class="game-desc">Покори дороги Европы за рулём легендарных грузовиков. Более 60 городов и бесконечные маршруты.</p>
          <div class="game-footer">
            <div class="game-price-block">
              <div class="game-price">₽ 599</div>
              <div class="game-rating">★ 4.9</div>
            </div>
            <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="btn-buy">
              <svg class="icon-svg"><use href="#icon-steam"/></svg>
              Купить
            </a>
          </div>
        </div>
      </div>
      
      <!-- ATS -->
      <div class="game-card fade-in">
        <div class="game-cover">
          <svg class="scene" viewBox="0 0 400 220" preserveAspectRatio="xMidYMid slice">
            <defs>
              <linearGradient id="atsbg" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#dc2626"/>
                <stop offset="100%" style="stop-color:#f97316"/>
              </linearGradient>
            </defs>
            <rect width="400" height="220" fill="url(#atsbg)"/>
            <polygon points="0,160 100,90 180,130 260,70 340,120 400,90 400,220 0,220" fill="#7c2d12" opacity="0.6"/>
            <polygon points="100,220 300,220 250,130 150,130" fill="#1f2937"/>
            <line x1="200" y1="220" x2="200" y2="130" stroke="#ffcc00" stroke-width="2" stroke-dasharray="10,10"/>
            <rect x="160" y="130" width="80" height="50" fill="#1e40af"/>
            <rect x="170" y="140" width="60" height="20" fill="#60a5fa" opacity="0.6"/>
            <rect x="160" y="180" width="80" height="15" fill="#1e3a8a"/>
            <circle cx="175" cy="200" r="8" fill="#000"/>
            <circle cx="225" cy="200" r="8" fill="#000"/>
            <rect x="50" y="140" width="8" height="40" fill="#166534"/>
            <rect x="45" y="150" width="5" height="15" fill="#166534"/>
            <rect x="60" y="145" width="5" height="20" fill="#166534"/>
          </svg>
          <span class="game-badge">Новинка</span>
          <span class="steam-overlay"><svg class="icon-svg"><use href="#icon-steam"/></svg>Steam</span>
        </div>
        <div class="game-info">
          <h3 class="game-title">American Truck Simulator</h3>
          <div class="game-meta">
            <span>🇺🇸 Америка</span>
            <span>🚛 Peterbilt, Kenworth</span>
          </div>
          <p class="game-desc">Легендарные американские грузовики и бескрайние просторы США. От Калифорнии до Невады.</p>
          <div class="game-footer">
            <div class="game-price-block">
              <div class="game-price">₽ 799</div>
              <div class="game-rating">★ 4.8</div>
            </div>
            <a href="https://store.steampowered.com/app/270880/American_Truck_Simulator/" target="_blank" rel="noopener" class="btn-buy">
              <svg class="icon-svg"><use href="#icon-steam"/></svg>
              Купить
            </a>
          </div>
        </div>
      </div>
      
      <!-- SnowRunner -->
      <div class="game-card fade-in">
        <div class="game-cover">
          <svg class="scene" viewBox="0 0 400 220" preserveAspectRatio="xMidYMid slice">
            <defs>
              <linearGradient id="snowbg" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#1e3a5f"/>
                <stop offset="100%" style="stop-color:#475569"/>
              </linearGradient>
            </defs>
            <rect width="400" height="220" fill="url(#snowbg)"/>
            <polygon points="0,140 80,80 160,120 240,60 320,100 400,70 400,220 0,220" fill="#e2e8f0" opacity="0.8"/>
            <polygon points="0,170 100,120 200,160 300,110 400,150 400,220 0,220" fill="#cbd5e1"/>
            <rect x="0" y="180" width="400" height="40" fill="#44403c"/>
            <rect x="150" y="130" width="100" height="55" fill="#dc2626"/>
            <rect x="160" y="140" width="30" height="20" fill="#60a5fa" opacity="0.6"/>
            <circle cx="170" cy="195" r="12" fill="#000"/>
            <circle cx="230" cy="195" r="12" fill="#000"/>
            <circle cx="170" cy="195" r="6" fill="#666"/>
            <circle cx="230" cy="195" r="6" fill="#666"/>
            <circle cx="50" cy="50" r="2" fill="white"/>
            <circle cx="120" cy="30" r="2" fill="white"/>
            <circle cx="200" cy="60" r="2" fill="white"/>
            <circle cx="280" cy="40" r="2" fill="white"/>
            <circle cx="350" cy="70" r="2" fill="white"/>
            <circle cx="80" cy="100" r="2" fill="white"/>
            <circle cx="320" cy="110" r="2" fill="white"/>
          </svg>
          <span class="game-badge">Топ</span>
          <span class="steam-overlay"><svg class="icon-svg"><use href="#icon-steam"/></svg>Steam</span>
        </div>
        <div class="game-info">
          <h3 class="game-title">SnowRunner</h3>
          <div class="game-meta">
            <span>❄️ Экстрим</span>
            <span>🚚 Off-road</span>
          </div>
          <p class="game-desc">Брось вызов снегу, грязи и бездорожью. Преодолевай невозможное на мощных внедорожниках.</p>
          <div class="game-footer">
            <div class="game-price-block">
              <div class="game-price">₽ 1299</div>
              <div class="game-rating">★ 4.7</div>
            </div>
            <a href="https://store.steampowered.com/app/1465360/SnowRunner/" target="_blank" rel="noopener" class="btn-buy">
              <svg class="icon-svg"><use href="#icon-steam"/></svg>
              Купить
            </a>
          </div>
        </div>
      </div>
      
      <!-- Farming Simulator -->
      <div class="game-card fade-in">
        <div class="game-cover">
          <svg class="scene" viewBox="0 0 400 220" preserveAspectRatio="xMidYMid slice">
            <defs>
              <linearGradient id="farmbg" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#ca8a04"/>
                <stop offset="100%" style="stop-color:#65a30d"/>
              </linearGradient>
            </defs>
            <rect width="400" height="220" fill="url(#farmbg)"/>
            <rect x="0" y="140" width="400" height="80" fill="#a16207"/>
            <line x1="0" y1="160" x2="400" y2="160" stroke="#854d0e" stroke-width="1"/>
            <line x1="0" y1="180" x2="400" y2="180" stroke="#854d0e" stroke-width="1"/>
            <line x1="0" y1="200" x2="400" y2="200" stroke="#854d0e" stroke-width="1"/>
            <circle cx="330" cy="60" r="30" fill="#fbbf24" opacity="0.9"/>
            <rect x="150" y="130" width="80" height="40" fill="#dc2626"/>
            <rect x="160" y="110" width="40" height="25" fill="#1e40af"/>
            <rect x="165" y="115" width="30" height="15" fill="#60a5fa" opacity="0.6"/>
            <circle cx="170" cy="180" r="15" fill="#000"/>
            <circle cx="220" cy="180" r="20" fill="#000"/>
            <circle cx="170" cy="180" r="7" fill="#666"/>
            <circle cx="220" cy="180" r="10" fill="#666"/>
          </svg>
          <span class="steam-overlay"><svg class="icon-svg"><use href="#icon-steam"/></svg>Steam</span>
        </div>
        <div class="game-info">
          <h3 class="game-title">Farming Simulator 25</h3>
          <div class="game-meta">
            <span>🌾 Ферма</span>
            <span>🚜 John Deere</span>
          </div>
          <p class="game-desc">Построй свою ферму мечты. Современная техника, сотни машин и бескрайние поля.</p>
          <div class="game-footer">
            <div class="game-price-block">
              <div class="game-price">₽ 1999</div>
              <div class="game-rating">★ 4.6</div>
            </div>
            <a href="https://store.steampowered.com/app/2449820/Farming_Simulator_25/" target="_blank" rel="noopener" class="btn-buy">
              <svg class="icon-svg"><use href="#icon-steam"/></svg>
              Купить
            </a>
          </div>
        </div>
      </div>
      
      <!-- MudRunner -->
      <div class="game-card fade-in">
        <div class="game-cover">
          <svg class="scene" viewBox="0 0 400 220" preserveAspectRatio="xMidYMid slice">
            <defs>
              <linearGradient id="mudbg" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#44403c"/>
                <stop offset="100%" style="stop-color:#78350f"/>
              </linearGradient>
            </defs>
            <rect width="400" height="220" fill="url(#mudbg)"/>
            <polygon points="0,150 40,100 80,140 120,90 160,130 200,80 240,120 280,90 320,130 360,100 400,140 400,220 0,220" fill="#14532d" opacity="0.7"/>
            <ellipse cx="200" cy="200" rx="180" ry="20" fill="#451a03"/>
            <ellipse cx="150" cy="195" rx="40" ry="8" fill="#78350f"/>
            <ellipse cx="260" cy="200" rx="50" ry="10" fill="#78350f"/>
            <rect x="160" y="140" width="90" height="45" fill="#b91c1c"/>
            <rect x="170" y="150" width="30" height="18" fill="#60a5fa" opacity="0.5"/>
            <circle cx="175" cy="195" r="13" fill="#000"/>
            <circle cx="235" cy="195" r="13" fill="#000"/>
            <circle cx="140" cy="185" r="4" fill="#451a03"/>
            <circle cx="270" cy="180" r="5" fill="#451a03"/>
            <circle cx="280" cy="190" r="3" fill="#451a03"/>
          </svg>
          <span class="steam-overlay"><svg class="icon-svg"><use href="#icon-steam"/></svg>Steam</span>
        </div>
        <div class="game-info">
          <h3 class="game-title">MudRunner</h3>
          <div class="game-meta">
            <span>💦 Бездорожье</span>
            <span>🚙 Off-road</span>
          </div>
          <p class="game-desc">Предшественник SnowRunner. Покоряй самые сложные трассы в одиночку или с друзьями.</p>
          <div class="game-footer">
            <div class="game-price-block">
              <div class="game-price">₽ 899</div>
              <div class="game-rating">★ 4.5</div>
            </div>
            <a href="https://store.steampowered.com/app/675010/MudRunner/" target="_blank" rel="noopener" class="btn-buy">
              <svg class="icon-svg"><use href="#icon-steam"/></svg>
              Купить
            </a>
          </div>
        </div>
      </div>
      
      <!-- Bus Simulator -->
      <div class="game-card fade-in">
        <div class="game-cover">
          <svg class="scene" viewBox="0 0 400 220" preserveAspectRatio="xMidYMid slice">
            <defs>
              <linearGradient id="busbg" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#7c3aed"/>
                <stop offset="100%" style="stop-color:#2563eb"/>
              </linearGradient>
            </defs>
            <rect width="400" height="220" fill="url(#busbg)"/>
            <rect x="20" y="100" width="40" height="100" fill="#1e293b"/>
            <rect x="70" y="80" width="50" height="120" fill="#334155"/>
            <rect x="130" y="110" width="40" height="90" fill="#1e293b"/>
            <rect x="280" y="90" width="50" height="110" fill="#334155"/>
            <rect x="340" y="120" width="40" height="80" fill="#1e293b"/>
            <rect x="30" y="110" width="8" height="8" fill="#fbbf24"/>
            <rect x="45" y="130" width="8" height="8" fill="#fbbf24"/>
            <rect x="85" y="95" width="8" height="8" fill="#fbbf24"/>
            <rect x="100" y="115" width="8" height="8" fill="#fbbf24"/>
            <rect x="0" y="180" width="400" height="40" fill="#1f2937"/>
            <line x1="0" y1="200" x2="400" y2="200" stroke="#ffcc00" stroke-width="2" stroke-dasharray="15,15"/>
            <rect x="160" y="140" width="120" height="50" fill="#fbbf24"/>
            <rect x="170" y="150" width="15" height="15" fill="#60a5fa" opacity="0.7"/>
            <rect x="190" y="150" width="15" height="15" fill="#60a5fa" opacity="0.7"/>
            <rect x="210" y="150" width="15" height="15" fill="#60a5fa" opacity="0.7"/>
            <rect x="230" y="150" width="15" height="15" fill="#60a5fa" opacity="0.7"/>
            <rect x="250" y="150" width="15" height="15" fill="#60a5fa" opacity="0.7"/>
            <circle cx="180" cy="195" r="8" fill="#000"/>
            <circle cx="260" cy="195" r="8" fill="#000"/>
          </svg>
          <span class="steam-overlay"><svg class="icon-svg"><use href="#icon-steam"/></svg>Steam</span>
        </div>
        <div class="game-info">
          <h3 class="game-title">Bus Simulator 21</h3>
          <div class="game-meta">
            <span>🚌 Город</span>
            <span>🚏 Маршруты</span>
          </div>
          <p class="game-desc">Стань лучшим водителем автобуса. Управляй собственной транспортной компанией.</p>
          <div class="game-footer">
            <div class="game-price-block">
              <div class="game-price">₽ 1499</div>
              <div class="game-rating">★ 4.4</div>
            </div>
            <a href="https://store.steampowered.com/app/1241960/Bus_Simulator_21/" target="_blank" rel="noopener" class="btn-buy">
              <svg class="icon-svg"><use href="#icon-steam"/></svg>
              Купить
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FEATURED -->
<section class="featured" id="featured">
  <div class="container">
    <div class="featured-grid">
      <div class="featured-visual fade-in">
        <span class="featured-tag">⭐ Игра месяца</span>
        <svg viewBox="0 0 640 400" preserveAspectRatio="xMidYMid slice">
          <defs>
            <linearGradient id="featbg" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" style="stop-color:#0f172a"/>
              <stop offset="50%" style="stop-color:#1e3a8a"/>
              <stop offset="100%" style="stop-color:#3b82f6"/>
            </linearGradient>
            <radialGradient id="featglow">
              <stop offset="0%" style="stop-color:#ff6b1a;stop-opacity:0.6"/>
              <stop offset="100%" style="stop-color:#ff6b1a;stop-opacity:0"/>
            </radialGradient>
          </defs>
          <rect width="640" height="400" fill="url(#featbg)"/>
          <circle cx="320" cy="200" r="200" fill="url(#featglow)"/>
          <polygon points="0,280 100,180 200,240 300,150 400,220 500,170 600,230 640,200 640,400 0,400" fill="#0f172a" opacity="0.8"/>
          <polygon points="0,320 120,240 240,300 360,220 480,280 600,240 640,270 640,400 0,400" fill="#020617"/>
          <polygon points="200,400 440,400 380,250 260,250" fill="#1f2937"/>
          <line x1="320" y1="400" x2="320" y2="250" stroke="#ffcc00" stroke-width="3" stroke-dasharray="15,15"/>
          <rect x="250" y="220" width="140" height="80" fill="#ff6b1a"/>
          <rect x="260" y="235" width="50" height="30" fill="#60a5fa" opacity="0.7"/>
          <rect x="320" y="235" width="60" height="30" fill="#1e293b" opacity="0.3"/>
          <circle cx="280" cy="315" r="18" fill="#000"/>
          <circle cx="360" cy="315" r="18" fill="#000"/>
          <circle cx="280" cy="315" r="8" fill="#666"/>
          <circle cx="360" cy="315" r="8" fill="#666"/>
          <circle cx="100" cy="60" r="2" fill="white"/>
          <circle cx="200" cy="40" r="1.5" fill="white"/>
          <circle cx="450" cy="70" r="2" fill="white"/>
          <circle cx="550" cy="50" r="1.5" fill="white"/>
          <circle cx="600" cy="100" r="2" fill="white"/>
          <circle cx="520" cy="80" r="30" fill="#fef3c7" opacity="0.9"/>
          <circle cx="510" cy="75" r="25" fill="url(#featbg)"/>
        </svg>
      </div>
      
      <div class="featured-content fade-in">
        <span class="section-tag">// Рекомендуем</span>
        <h2>Euro Truck <span>Simulator 2</span></h2>
        <p>Самый популярный симулятор дальнобойщика в мире. Более 10 лет развития, миллионы игроков и бесконечные возможности для кастомизации.</p>
        
        <ul class="feature-list">
          <li>Более 70 городов Европы</li>
          <li>Официальные лицензии грузовиков</li>
          <li>Реалистичная физика и графика</li>
          <li>Моддинг-сообщество с тысячами модов</li>
          <li>Мультиплеер через TruckersMP</li>
        </ul>
        
        <div class="featured-buttons">
          <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="btn btn-steam">
            <svg class="icon-svg"><use href="#icon-steam"/></svg>
            Купить в Steam
          </a>
          <a href="https://www.youtube.com/results?search_query=euro+truck+simulator+2+trailer" target="_blank" rel="noopener" class="btn btn-outline">
            ▶ Трейлер
          </a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- NEWS -->
<section id="news">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">// Последние новости</span>
      <h2 class="section-title">Что <span>нового</span></h2>
      <p class="section-desc">Обновления, релизы и события из мира симуляторов</p>
    </div>
    
    <div class="news-grid">
      <article class="news-card fade-in">
        <div class="news-image">
          <svg viewBox="0 0 400 180" preserveAspectRatio="xMidYMid slice">
            <rect width="400" height="180" fill="#1e3a8a"/>
            <polygon points="0,120 80,60 160,100 240,40 320,90 400,60 400,180 0,180" fill="#0f172a"/>
            <rect x="150" y="90" width="100" height="50" fill="#ff6b1a"/>
            <circle cx="170" cy="150" r="10" fill="#000"/>
            <circle cx="230" cy="150" r="10" fill="#000"/>
          </svg>
          <span class="news-category">Обновление</span>
        </div>
        <div class="news-content">
          <div class="news-date">08 Октября 2026</div>
          <h3 class="news-title">ETS 2: Новый DLC Iberia уже доступен</h3>
          <p class="news-excerpt">Португалия и Испания теперь доступны для прохождения. Новые города, грузы и задания.</p>
          <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="read-more">В Steam →</a>
        </div>
      </article>
      
      <article class="news-card fade-in">
        <div class="news-image">
          <svg viewBox="0 0 400 180" preserveAspectRatio="xMidYMid slice">
            <rect width="400" height="180" fill="#7c2d12"/>
            <polygon points="0,100 100,50 200,90 300,40 400,80 400,180 0,180" fill="#451a03"/>
            <rect x="150" y="80" width="100" height="60" fill="#dc2626"/>
            <circle cx="170" cy="150" r="12" fill="#000"/>
            <circle cx="230" cy="150" r="12" fill="#000"/>
            <circle cx="100" cy="30" r="3" fill="white"/>
            <circle cx="300" cy="40" r="3" fill="white"/>
          </svg>
          <span class="news-category">Анонс</span>
        </div>
        <div class="news-content">
          <div class="news-date">05 Октября 2026</div>
          <h3 class="news-title">SnowRunner 2 — первый тизер</h3>
          <p class="news-excerpt">Saber Interactive анонсировала продолжение культового off-road симулятора. Релиз в 2027 году.</p>
          <a href="https://store.steampowered.com/app/1465360/SnowRunner/" target="_blank" rel="noopener" class="read-more">В Steam →</a>
        </div>
      </article>
      
      <article class="news-card fade-in">
        <div class="news-image">
          <svg viewBox="0 0 400 180" preserveAspectRatio="xMidYMid slice">
            <rect width="400" height="180" fill="#dc2626"/>
            <polygon points="0,140 100,80 200,120 300,70 400,110 400,180 0,180" fill="#7c2d12"/>
            <rect x="140" y="90" width="120" height="50" fill="#1e40af"/>
            <rect x="150" y="100" width="40" height="20" fill="#60a5fa" opacity="0.6"/>
            <circle cx="160" cy="150" r="10" fill="#000"/>
            <circle cx="240" cy="150" r="10" fill="#000"/>
          </svg>
          <span class="news-category">Событие</span>
        </div>
        <div class="news-content">
          <div class="news-date">01 Октября 2026</div>
          <h3 class="news-title">TruckersMP: Тур по Европе собрал 10K игроков</h3>
          <p class="news-excerpt">Масштабное онлайн-событие объединило тысячи дальнобойщиков со всего мира на маршруте Париж-Берлин.</p>
          <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="read-more">В Steam →</a>
        </div>
      </article>
      
      <article class="news-card fade-in">
        <div class="news-image">
          <svg viewBox="0 0 400 180" preserveAspectRatio="xMidYMid slice">
            <rect width="400" height="180" fill="#ca8a04"/>
            <rect x="0" y="120" width="400" height="60" fill="#a16207"/>
            <rect x="140" y="80" width="120" height="50" fill="#dc2626"/>
            <rect x="150" y="60" width="50" height="25" fill="#1e40af"/>
            <circle cx="160" cy="140" r="12" fill="#000"/>
            <circle cx="240" cy="140" r="15" fill="#000"/>
            <circle cx="330" cy="50" r="25" fill="#fbbf24" opacity="0.9"/>
          </svg>
          <span class="news-category">Гайд</span>
        </div>
        <div class="news-content">
          <div class="news-date">28 Сентября 2026</div>
          <h3 class="news-title">Топ-10 модов для Farming Simulator 25</h3>
          <p class="news-excerpt">Подборка лучших модификаций, которые сделают вашу ферму ещё реалистичнее и интереснее.</p>
          <a href="https://store.steampowered.com/app/2449820/Farming_Simulator_25/" target="_blank" rel="noopener" class="read-more">В Steam →</a>
        </div>
      </article>
    </div>
  </div>
</section>

<!-- COMMUNITY -->
<section class="community" id="community">
  <div class="container">
    <div class="section-header fade-in">
      <span class="section-tag">// Присоединяйся</span>
      <h2 class="section-title">Наше <span>Сообщество</span></h2>
      <p class="section-desc">Тысячи игроков уже с нами. Стань частью самой большой семьи дальнобойщиков</p>
    </div>
    
    <div class="community-grid">
      <a href="https://lolka.gg/GLJyH2hld" target="_blank" rel="noopener" class="community-card lolka fade-in">
        <div class="community-icon">
          <svg viewBox="0 0 24 24">
            <defs>
              <linearGradient id="lolkaGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" style="stop-color:#fff"/>
                <stop offset="100%" style="stop-color:#ffd6f5"/>
              </linearGradient>
            </defs>
            <circle cx="12" cy="12" r="10" fill="none" stroke="url(#lolkaGrad)" stroke-width="1.5"/>
            <text x="12" y="16" text-anchor="middle" fill="white" font-family="Orbitron" font-size="10" font-weight="900">L</text>
            <circle cx="17" cy="7" r="2.5" fill="#ff1493"/>
          </svg>
        </div>
        <h3>Lolka</h3>
        <p>Мой канал в приложении Lolka — общайся и смотри контент</p>
        <div class="community-stat">Подпишись</div>
      </a>
      
      <a href="https://www.youtube.com/channel/UCGmGqREpWDBe0wSDSenw7Kg" target="_blank" rel="noopener" class="community-card youtube fade-in">
        <div class="community-icon">
          <svg><use href="#icon-youtube"/></svg>
        </div>
        <h3>YouTube</h3>
        <p>Гайды, стримы и обзоры на моём канале</p>
        <div class="community-stat">Смотреть</div>
      </a>
      
      <a href="https://www.twitch.tv/nikolas_s2017" target="_blank" rel="noopener" class="community-card twitch fade-in">
        <div class="community-icon">
          <svg><use href="#icon-twitch"/></svg>
        </div>
        <h3>Twitch</h3>
        <p>Смотри мои прямые трансляции в реальном времени</p>
        <div class="community-stat">Live</div>
      </a>
      
      <a href="https://t.me/EuroTruck_Simulator_2" target="_blank" rel="noopener" class="community-card telegram fade-in">
        <div class="community-icon">
          <svg><use href="#icon-telegram"/></svg>
        </div>
        <h3>Telegram</h3>
        <p>Новости, анонсы и общение в Telegram-канале</p>
        <div class="community-stat">Вступить</div>
      </a>
    </div>
    
    <div style="text-align:center; margin-top:3rem; display:flex; gap:1rem; justify-content:center; flex-wrap:wrap;">
      <a href="https://lolka.gg/GLJyH2hld" target="_blank" rel="noopener" class="btn">🎮 Перейти в Lolka</a>
      <a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener" class="btn btn-steam">
        <svg class="icon-svg"><use href="#icon-steam"/></svg>
        Steam
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-content">
    <div class="footer-col footer-about">
      <div class="logo">
        <div class="logo-icon"></div>
        TRUCK SIM HUB
      </div>
      <p>Главный портал для фанатов симуляторов грузовиков и внедорожной техники. Новости, гайды, сообщество и многое другое.</p>
      <div class="social-links">
        <a href="https://lolka.gg/GLJyH2hld" target="_blank" rel="noopener" title="Lolka" class="lolka">
          <svg viewBox="0 0 24 24">
            <circle cx="12" cy="12" r="10" fill="none" stroke="white" stroke-width="1.5"/>
            <text x="12" y="16" text-anchor="middle" fill="white" font-family="Orbitron" font-size="10" font-weight="900">L</text>
            <circle cx="17" cy="7" r="2.5" fill="#ff1493"/>
          </svg>
        </a>
        <a href="https://www.youtube.com/channel/UCGmGqREpWDBe0wSDSenw7Kg" target="_blank" rel="noopener" title="YouTube" class="youtube">
          <svg><use href="#icon-youtube"/></svg>
        </a>
        <a href="https://www.twitch.tv/nikolas_s2017" target="_blank" rel="noopener" title="Twitch" class="twitch">
          <svg><use href="#icon-twitch"/></svg>
        </a>
        <a href="https://t.me/EuroTruck_Simulator_2" target="_blank" rel="noopener" title="Telegram" class="telegram">
          <svg><use href="#icon-telegram"/></svg>
        </a>
      </div>
    </div>
    
    <div class="footer-col">
      <h4>Игры в Steam</h4>
      <ul>
        <li><a href="https://store.steampowered.com/app/227300/Euro_Truck_Simulator_2/" target="_blank" rel="noopener">Euro Truck Sim 2</a></li>
        <li><a href="https://store.steampowered.com/app/270880/American_Truck_Simulator/" target="_blank" rel="noopener">American Truck Sim</a></li>
        <li><a href="https://store.steampowered.com/app/1465360/SnowRunner/" target="_blank" rel="noopener">SnowRunner</a></li>
        <li><a href="https://store.steampowered.com/app/2449820/Farming_Simulator_25/" target="_blank" rel="noopener">Farming Sim 25</a></li>
        <li><a href="https://store.steampowered.com/app/675010/MudRunner/" target="_blank" rel="noopener">MudRunner</a></li>
        <li><a href="https://store.steampowered.com/app/1241960/Bus_Simulator_21/" target="_blank" rel="noopener">Bus Simulator 21</a></li>
      </ul>
    </div>
    
    <div class="footer-col">
      <h4>Сообщество</h4>
      <ul>
        <li><a href="https://lolka.gg/GLJyH2hld" target="_blank" rel="noopener">Lolka</a></li>
        <li><a href="https://www.youtube.com/channel/UCGmGqREpWDBe0wSDSenw7Kg" target="_blank" rel="noopener">YouTube</a></li>
        <li><a href="https://www.twitch.tv/nikolas_s2017" target="_blank" rel="noopener">Twitch</a></li>
        <li><a href="https://t.me/EuroTruck_Simulator_2" target="_blank" rel="noopener">Telegram</a></li>
        <li><a href="https://store.steampowered.com/" target="_blank" rel="noopener">Steam</a></li>
      </ul>
    </div>
    
    <div class="footer-col">
      <h4>Инфо</h4>
      <ul>
        <li><a href="#">О нас</a></li>
        <li><a href="#">Контакты</a></li>
        <li><a href="#">Реклама</a></li>
        <li><a href="#">Политика</a></li>
        <li><a href="#">FAQ</a></li>
      </ul>
    </div>
  </div>
  
  <div class="footer-bottom">
    © 2026 TRUCK SIM HUB. Все права защищены. Сделано с ❤️ для фанатов грузовиков.
  </div>
</footer>

<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });
  
  document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
  
  const nav = document.querySelector('nav');
  window.addEventListener('scroll', () => {
    if (window.scrollY > 50) {
      nav.style.background = 'rgba(5, 7, 13, 0.95)';
      nav.style.boxShadow = '0 5px 30px rgba(255,107,26,0.1)';
    } else {
      nav.style.background = 'rgba(5, 7, 13, 0.85)';
      nav.style.boxShadow = 'none';
    }
  });
  
  const counters = document.querySelectorAll('.stat-num');
  const animateCounter = (el) => {
    const text = el.textContent;
    const numMatch = text.match(/\d+/);
    if (!numMatch) return;
    const target = parseInt(numMatch[0]);
    const suffix = text.replace(/\d+/, '');
    let current = 0;
    const step = target / 40;
    const interval = setInterval(() => {
      current += step;
      if (current >= target) {
        current = target;
        clearInterval(interval);
      }
      el.textContent = Math.floor(current) + suffix;
    }, 30);
  };
  
  const statsObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        animateCounter(entry.target);
        statsObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.5 });
  
  counters.forEach(c => statsObserver.observe(c));
  
  // Smooth scroll только для якорных ссылок
  document.querySelectorAll('a[href^="#"]').forEach(link => {
    link.addEventListener('click', (e) => {
      const href = link.getAttribute('href');
      if (href && href.length > 1) {
        e.preventDefault();
        const target = document.querySelector(href);
        if (target) {
          target.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }
      }
    });
  });
  
  const menuToggle = document.querySelector('.menu-toggle');
  const navLinks = document.querySelector('.nav-links');
  if (menuToggle && navLinks) {
    menuToggle.addEventListener('click', () => {
      if (navLinks.style.display === 'flex') {
        navLinks.style.display = '';
        navLinks.style.flexDirection = '';
        navLinks.style.position = '';
        navLinks.style.top = '';
        navLinks.style.left = '';
        navLinks.style.right = '';
        navLinks.style.background = '';
        navLinks.style.padding = '';
      } else {
        navLinks.style.display = 'flex';
        navLinks.style.flexDirection = 'column';
        navLinks.style.position = 'absolute';
        navLinks.style.top = '100%';
        navLinks.style.left = '0';
        navLinks.style.right = '0';
        navLinks.style.background = 'rgba(5,7,13,0.98)';
        navLinks.style.padding = '1rem';
      }
    });
  }
</script>

</body>
</html>
b
