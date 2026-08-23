<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blackout City - Roleplay Community</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: #030303; color: #ffffff; min-height: 100vh; padding-bottom: 50px; overflow-x: hidden; }
        
        /* Navigation Bar */
        nav { display: flex; justify-content: space-between; align-items: center; padding: 20px 50px; background: rgba(3,3,3,0.95); border-bottom: 1px solid rgba(255, 59, 48, 0.2); position: sticky; top: 0; z-index: 100; backdrop-filter: blur(12px); }
        
        /* Server Logo Styling */
        .nav-logo { display: flex; align-items: center; gap: 14px; text-decoration: none; cursor: pointer; }
        .server-logo-img { width: 42px; height: 42px; border-radius: 50%; object-fit: cover; border: 2px solid #ff3b30; box-shadow: 0 0 15px rgba(255, 59, 48, 0.5); }
        .nav-logo span { font-size: 19px; font-weight: 900; color: #fff; letter-spacing: 2.5px; text-transform: uppercase; text-shadow: 0 0 10px rgba(255, 59, 48, 0.4); }

        .nav-links { display: flex; gap: 30px; align-items: center; }
        nav a:not(.nav-logo) { color: #999; text-decoration: none; font-size: 12px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; transition: 0.3s ease; }
        nav a:not(.nav-logo):hover, nav a.active { color: #fff; text-shadow: 0 0 12px rgba(255, 59, 48, 0.8); }

        /* Home Hero Banner */
        .home-hero-container { text-align: center; padding: 80px 20px 40px; }
        .big-server-logo { width: 170px; height: 170px; border-radius: 50%; object-fit: cover; border: 3px solid #ff3b30; box-shadow: 0 0 40px rgba(255, 59, 48, 0.6); margin-bottom: 25px; animation: pulseGlow 2.5s infinite; }
        @keyframes pulseGlow {
            0% { box-shadow: 0 0 20px rgba(255, 59, 48, 0.4); transform: scale(1); }
            50% { box-shadow: 0 0 45px rgba(255, 59, 48, 0.8); transform: scale(1.02); }
            100% { box-shadow: 0 0 20px rgba(255, 59, 48, 0.4); transform: scale(1); }
        }
        .welcome-title { font-size: 34px; text-transform: uppercase; font-weight: 900; letter-spacing: 3px; color: #ffffff; text-shadow: 0 0 20px rgba(255, 59, 48, 0.6); }

        /* Header Section */
        .header-section { text-align: center; padding: 40px 20px 20px; }
        h1 { font-size: 38px; text-transform: uppercase; font-weight: 900; letter-spacing: 3px; margin-bottom: 10px; background: linear-gradient(90deg, #ffffff, #ff3b30); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        p.subtitle { color: #888; font-size: 13px; text-transform: uppercase; letter-spacing: 2px; font-weight: 600; }
        
        /* View Sections */
        .page-view { display: none; padding: 20px 20px 40px; animation: fadeIn 0.4s ease-in-out; }
        .page-view.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }

        /* Rules Container */
        .rules-wrapper { max-width: 950px; margin: 0 auto; background: rgba(12, 12, 12, 0.95); border: 1px solid rgba(255, 59, 48, 0.2); border-radius: 14px; padding: 45px; box-shadow: 0 20px 50px rgba(0,0,0,0.8); backdrop-filter: blur(10px); }
        .rules-wrapper h2 { font-size: 26px; text-transform: uppercase; margin-bottom: 25px; color: #ff3b30; font-weight: 900; letter-spacing: 1.5px; border-bottom: 2px solid rgba(255, 59, 48, 0.4); padding-bottom: 12px; text-shadow: 0 0 10px rgba(255, 59, 48, 0.3); }
        .rule-item { margin-bottom: 22px; border-bottom: 1px solid rgba(255,255,255,0.05); padding-bottom: 18px; }
        .rule-item p { font-size: 14px; color: #ccc; line-height: 1.7; white-space: pre-line; letter-spacing: 0.3px; }

        /* Cards Container */
        .cards-container { display: flex; justify-content: center; gap: 25px; max-width: 1450px; margin: 20px auto; padding: 0 20px; flex-wrap: wrap; }
        .app-card { 
            width: 280px; height: 390px; position: relative; background-size: cover; background-position: center; 
            border: 1px solid rgba(255, 59, 48, 0.3); border-radius: 14px; padding: 30px 20px; display: flex; flex-direction: column; 
            justify-content: flex-end; text-decoration: none; overflow: hidden; transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1); cursor: pointer; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.7);
        }
        .app-card::after { 
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%; 
            background: linear-gradient(to top, rgba(3,3,3,0.95) 25%, rgba(3,3,3,0.5) 70%, rgba(3,3,3,0.2) 100%); z-index: 1; 
            transition: 0.3s;
        }
        .app-card > * { position: relative; z-index: 2; }
        .app-card:hover { border-color: #ff3b30; transform: translateY(-10px) scale(1.02); box-shadow: 0 20px 40px rgba(255, 59, 48, 0.4); }
        .app-card:hover::after { background: linear-gradient(to top, rgba(3,3,3,0.9) 30%, rgba(255,59,48,0.25) 100%); }
        .card-content h3 { font-size: 15px; font-weight: 900; text-transform: uppercase; color: #fff; letter-spacing: 1.5px; text-shadow: 0 2px 5px rgba(0,0,0,0.8); }

        /* Form Layout */
        .form-wrapper { max-width: 700px; margin: 0 auto; background: rgba(12, 12, 12, 0.95); border: 1px solid rgba(255, 59, 48, 0.2); border-radius: 14px; padding: 45px; box-shadow: 0 20px 50px rgba(0,0,0,0.8); backdrop-filter: blur(10px); }
        .form-wrapper h2 { font-size: 24px; text-transform: uppercase; margin-bottom: 8px; color: #fff; font-weight: 900; letter-spacing: 1px; }
        .form-wrapper p.desc { font-size: 12px; color: #888; text-transform: uppercase; margin-bottom: 25px; border-bottom: 2px solid rgba(255, 59, 48, 0.4); padding-bottom: 10px; letter-spacing: 1px; font-weight: 600; }
        .input-group { margin-bottom: 22px; }
        label { display: block; font-size: 12px; font-weight: bold; text-transform: uppercase; margin-bottom: 8px; color: #ccc; letter-spacing: 1px; }
        input, select, textarea { width: 100%; padding: 14px; background: rgba(20, 20, 20, 0.9); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 8px; color: #fff; font-size: 14px; transition: 0.3s; }
        input:focus, select:focus, textarea:focus { border-color: #ff3b30; outline: none; box-shadow: 0 0 10px rgba(255, 59, 48, 0.3); }
        textarea { resize: vertical; height: 110px; }
        .submit-btn { background: linear-gradient(90deg, #ff2a2a, #ff3b30); color: white; border: none; padding: 16px; font-size: 14px; font-weight: bold; text-transform: uppercase; border-radius: 8px; cursor: pointer; width: 100%; transition: 0.3s; margin-top: 10px; letter-spacing: 1.5px; box-shadow: 0 5px 20px rgba(255, 59, 48, 0.4); }
        .submit-btn:hover { opacity: 0.95; transform: translateY(-2px); box-shadow: 0 8px 25px rgba(255, 59, 48, 0.6); }
        .back-btn { display: inline-block; margin-top: 25px; color: #888; text-decoration: none; font-size: 12px; text-transform: uppercase; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .back-btn:hover { color: #fff; }
    </style>
</head>
<body>

    <!-- Navbar -->
    <nav>
        <a class="nav-logo" onclick="showView('home')">
            <img src="https://i.ibb.co/Fb4M1cNz/content.png" alt="Blackout City Logo" class="server-logo-img">
            <span>BLACKOUT CITY</span>
        </a>
        <div class="nav-links">
            <a onclick="showView('home')" id="link-home" class="active">Home</a>
            <a onclick="showView('applications')" id="link-apps">Blackout City Application</a>
            <a onclick="showView('rules')" id="link-rules">Rules</a>
            <a onclick="showView('home')">Team</a>
        </div>
    </nav>

    <!-- Home Section -->
    <div id="home" class="page-view active">
        <div class="home-hero-container">
            <img src="https://i.ibb.co/Fb4M1cNz/content.png" alt="Blackout City Big Logo" class="big-server-logo">
            <div class="welcome-title">Welcome to Blackout City Roleplay</div>
        </div>
    </div>

    <!-- Rules Section -->
    <div id="rules" class="page-view">
        <div class="rules-wrapper">
            <h2>Server Rules & Regulations</h2>
            <div class="rule-item">
                <p>1. OOC : l chat mech maj3oula chte5ou/ta3ti biha infos HRP !
2. RDM : Ma 3andekch el 7a9 to9tel Player men ghir sbab !
3. VDM :  ma 3andekch el 7a9 testa3mel vehicle bech to9tel wala tadhreb player
4. VOL :  lezmek dima tkhaf 3la l character mte3ek w t9ader 7yetou !
5. Power Gaming :  ma lezmekch tet9awa 3al character mte3ek :  
    - Example : Accident wela Tnagaz men blasa 3alya w tetwaja3ch 
6. Meta Gaming :  ma 3andekch el 7a9 testa3mel info makech makhedhha in game w kol info lazemha record snn meta !
7. Fail RP :  ma 3andekch el 7a9 ta3mel 7aja moch ma39oula w matemchich m3a character mte3ek !
8. Force RP :  ma 3andekch el 7a9 tet9awa 3la player bech tekhou advantage fi scene
    - Example : tfok info wela flous bl force
9. Win RP :  ma 3andekch el 7a9 tekhtare3 7ajet moch mawjoudin in game bech terba7 bihom scene
10. Combat Logging :  tleave l game wela ta3mal rou7ek afk fi west scene 
11. Combat Storing :  ma 3andekch el 7a9 tohreb l greenzone fi west scene (5alet 3lik chkoun wela fi fight)
12. Clear Shot :  famammech 7aja esmha clear shot fel RP ki yebda famma hostage
13. Revenge kill :  Ken makech f gang lazmek record & info rp & 2h bech tnajam ta3mal revenge !
14. Disrespect / Toxicity  : Interdit tetmanyak 3ala player w houwa taye7 (la b emote w la b klem) !
15. Use Rule :  tcouveri rou7ek b rule f scene 
   - Example : teprovoqui chkoun fi greenzone khater ta3ref maynajamch ya3malek chy
16. Pain RP :  ki tetdhrab wala ta3mel accident wala 3amaliya lezmek tetwaja3 w tetasarref kima IRL
17. Kofr rabbi bannable 7atta lawken bin las7ab ama saben ay 7ad mel 3ila bannable ken wsel fama report 
18. Abusing any glitch or finding one and not reporting it to the staff will result in a Permanent ban
19. Using any kind of third party cheats / mods that give you advantage visually will result in a Permanent ban
20. Any kind of sexual abuse or ra**ping scenes will result in an extremely severe sanction
21. Skipping a scene with an EMS, Police or lawyer will result in a ban
22. You must choose a realistic name otherwise you character will get deleted
23. Third party or free loot are not allowed
25. Mamnou3 tkhalli 7aja men amlekek l player ekhor ki bech tsirlek mort rp wela to5rej m server (zouz yet7asbou)
26. Ki tsirlek mort rp characterek jdid lezem ykoun ma 3andou 7atta 3ale9a bel character l 9dim
27. Ken 7ad faila m3ak tkammel scene w treporti fellekher (tnajam treporti meloul ama lazem tekteb "spectate")
28. Ay refund lazmou record
29. /me :  used to describe a feeling
30. /do :  used to describe an action
31. MASS RP :  Dima lazem t7ot f balek elli lemdina m3ebya (temchi l markez troll wa7dek 5atrou fera8 & etc..)
32. New Life Rule :  ki tmout bounya tetdhakar // ki tmout b sle7 abyadh tetdhakar mba3d 12h // ki tmout b pistol tensa scene kemla !
33. Fl server fama bnet zeda donc medhabina tofla 9aletch 9odemk klem zayed mat7kich 9odemha que ce soit mwajjeh liha wela msh liha si nn ban ken reportet heya.
34. Poor Quality = Unwhitelisted + Ban youssel 7ata Perma. (kima tabda tseb fi ay wehed ysceni m3ak w techri f chbouk, toxicity, tkarah player fel RP, tchouf tfol m3ah tofla temchi tetlakech 3lih w taya7lou 9adrou, any kind of tfourikh ...etc)
35. Emote fi west fight mamnou3a w BANNABLE.
37. Tangiz bl moto wela bl karhba mamnou3 w aalih ban POWER GAMING (tangiza ma39oula)
38. Fail Drive mawjouda: aajltin maflou9in = fail drive / karhba msh off road me tatlaach jbal (que ce soit diwena wela ml cardealer) ..etc
39. MIX RP:  tseb chkoun f discord alekhater sart maah scene in game wela sart maa chkoun mochkla discord w mshytlou in game bedhema = BAN 7days tousel lel Perma
40. Karhba maghir plate tnajamch ta5ouha repere. (ka police tnajam thezha l markez w ta9ra serie 8adi)</p>
            </div>
        </div>
    </div>

    <!-- Applications Hub Section -->
    <div id="applications" class="page-view">
        <div class="header-section">
            <h1>BLACKOUT CITY APPLICATIONS</h1>
            <p class="subtitle">Select a department to submit your official application directly to our team</p>
        </div>
        <div class="cards-container">
            <div class="app-card" onclick="showView('whitelist')" style="background-image: url('https://images.unsplash.com/photo-1450133064473-71024230f91b?auto=format&fit=crop&w=600&q=80');">
                <div class="card-content"><h3>Whitelist (Citizen)</h3></div>
            </div>
            <div class="app-card" onclick="showView('gang')" style="background-image: url('https://images.unsplash.com/photo-1563906267088-b029e7101114?auto=format&fit=crop&w=600&q=80');">
                <div class="card-content"><h3>Gang & Family</h3></div>
            </div>
            <div class="app-card" onclick="showView('police')" style="background-image: url('https://images.unsplash.com/photo-1589829545856-d10d557cf95f?auto=format&fit=crop&w=600&q=80');">
                <div class="card-content"><h3>Police Department</h3></div>
            </div>
            <div class="app-card" onclick="showView('ems')" style="background-image: url('https://images.unsplash.com/photo-1584515979956-d9f6e5d09982?auto=format&fit=crop&w=600&q=80');">
                <div class="card-content"><h3>EMS Department</h3></div>
            </div>
        </div>
    </div>

    <!-- Whitelist Form View -->
    <div id="whitelist" class="page-view">
        <div class="form-wrapper">
            <h2>Whitelist Application</h2>
            <p class="desc">Submit your citizenship request</p>
            <form id="whitelistForm" class="application-form" data-form-name="Whitelist Application">
                <div class="input-group"><label>Real Name</label><input type="text" name="Real Name" required></div>
                <div class="input-group"><label>Character Name</label><input type="text" name="Character Name" required></div>
                <div class="input-group"><label>Age</label><input type="number" name="Age" required></div>
                <div class="input-group"><label>Discord ID</label><input type="text" name="Discord ID" required></div>
                <div class="input-group"><label>Character Backstory</label><textarea name="Character Backstory" required></textarea></div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('applications')">&larr; Back to Applications</a>
        </div>
    </div>

    <!-- Gang Form View -->
    <div id="gang" class="page-view">
        <div class="form-wrapper">
            <h2>Gang / Org Application</h2>
            <p class="desc">Register your organization</p>
            <form id="gangForm" class="application-form" data-form-name="Gang Application">
                <div class="input-group"><label>Gang Name</label><input type="text" name="Gang Name" required></div>
                <div class="input-group"><label>Number of Members</label><input type="number" name="Number of Members" required></div>
                <div class="input-group"><label>Gang Backstory</label><textarea name="Gang Backstory" required></textarea></div>
                <div class="input-group"><label>Gang Goals</label><textarea name="Gang Goals" required></textarea></div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('applications')">&larr; Back to Applications</a>
        </div>
    </div>

    <!-- Police Form View -->
    <div id="police" class="page-view">
        <div class="form-wrapper">
            <h2>Police Department Application</h2>
            <p class="desc">Enforce law and order</p>
            <form id="policeForm" class="application-form" data-form-name="Police Application">
                <div class="input-group"><label>Character Name</label><input type="text" name="Character Name" required></div>
                <div class="input-group"><label>Why do you want to join the LSPD?</label><textarea name="Reason" required></textarea></div>
                <div class="input-group"><label>Have you ever been an officer before?</label><textarea name="Previous Experience" required></textarea></div>
                <div class="input-group"><label>Availability (Hours/Week)</label><input type="text" name="Availability" required></div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('applications')">&larr; Back to Applications</a>
        </div>
    </div>

    <!-- EMS Form View -->
    <div id="ems" class="page-view">
        <div class="form-wrapper">
            <h2>EMS Department Application</h2>
            <p class="desc">Provide medical services</p>
            <form id="emsForm" class="application-form" data-form-name="EMS Application">
                <div class="input-group"><label>Character Name</label><input type="text" name="Character Name" required></div>
                <div class="input-group"><label>Why do you want to join EMS?</label><textarea name="Reason" required></textarea></div>
                <div class="input-group"><label>Medical Knowledge / Experience</label><textarea name="Medical Experience" required></textarea></div>
                <div class="input-group"><label>Are you familiar with triage?</label>
                    <select name="Familiar with Triage"><option>Yes</option><option>No</option></select>
                </div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('applications')">&larr; Back to Applications</a>
        </div>
    </div>

    <script>
        function showView(viewId) {
            document.querySelectorAll('.page-view').forEach(v => v.classList.remove('active'));
            document.getElementById(viewId).classList.add('active');

            document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));
            if(viewId === 'home') {
                document.getElementById('link-home').classList.add('active');
            } else if(['applications', 'whitelist', 'gang', 'police', 'ems'].includes(viewId)) {
                document.getElementById('link-apps').classList.add('active');
            } else if(viewId === 'rules') {
                document.getElementById('link-rules').classList.add('active');
            }

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        document.getElementById('link-home').classList.add('active');

        // General Discord Webhook Integration for ALL Applications
        document.querySelectorAll('.application-form').forEach(form => {
            form.addEventListener('submit', function(e) {
                e.preventDefault();

                const formData = new FormData(form);
                const formName = form.getAttribute('data-form-name');
                const webhookUrl = 'https://discord.com/api/webhooks/1541103390258495630/PBKLm-Y-Ei3Qyl5LrGLCl8Gsf9XbEqKgHjJ0wh_IA-s6SdtVmCX4hVtCihM9acN3L_sH';

                let descriptionFields = "";
                formData.forEach((value, key) => {
                    descriptionFields += `> **${key}:** ${value}\n`;
                });

                const payload = {
                    content: `📋 **New ${formName} Received!**\n` + descriptionFields
                };

                fetch(webhookUrl, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(payload)
                }).then(response => {
                    if (response.ok) {
                        alert('Application Submitted Successfully to Discord!');
                        form.reset();
                        showView('applications');
                    } else {
                        alert('Error submitting application. Please try again.');
                    }
                }).catch(error => {
                    console.error('Error:', error);
                    alert('An error occurred.');
                });
            });
        });
    </script>
</body>
</html>
