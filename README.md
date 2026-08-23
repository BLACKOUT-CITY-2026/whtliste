<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blackout City Applications</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: #050505; color: #ffffff; min-height: 100vh; padding-bottom: 40px; overflow-x: hidden; }
        
        /* Navigation Bar */
        nav { display: flex; justify-content: space-between; align-items: center; padding: 20px 50px; background: rgba(5,5,5,0.95); border-bottom: 1px solid #1a1a1a; position: sticky; top: 0; z-index: 100; backdrop-filter: blur(10px); }
        
        /* Server Logo Styling */
        .nav-logo { display: flex; align-items: center; gap: 12px; text-decoration: none; cursor: pointer; }
        .server-logo-img { width: 40px; height: 40px; border-radius: 50%; object-fit: cover; border: 2px solid #ff4b2b; box-shadow: 0 0 10px rgba(255, 75, 43, 0.4); }
        .nav-logo span { font-size: 18px; font-weight: 900; color: #fff; letter-spacing: 2px; text-transform: uppercase; }

        .nav-links { display: flex; gap: 25px; align-items: center; }
        nav a:not(.nav-logo) { color: #888; text-decoration: none; font-size: 12px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; transition: 0.3s; }
        nav a:not(.nav-logo):hover, nav a.active { color: #fff; text-shadow: 0 0 10px rgba(255,255,255,0.5); }
        nav a.active { border-bottom: 2px solid #fff; padding-bottom: 4px; }

        /* Header Section */
        .header-section { text-align: center; padding: 50px 20px 30px; }
        h1 { font-size: 42px; text-transform: uppercase; font-weight: 900; letter-spacing: 3px; margin-bottom: 10px; background: linear-gradient(90deg, #ffffff, #ff4b2b); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        p.subtitle { color: #aaa; font-size: 13px; text-transform: uppercase; letter-spacing: 1.5px; font-weight: 600; }
        
        /* View Sections */
        .page-view { display: none; padding: 30px 20px; animation: fadeIn 0.4s ease-in-out; }
        .page-view.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Cards Container */
        .cards-container { display: flex; justify-content: center; gap: 20px; max-width: 1450px; margin: 30px auto; padding: 0 20px; flex-wrap: wrap; }
        
        .app-card { 
            width: 270px; height: 380px; position: relative; background-size: cover; background-position: center; 
            border: 1px solid #222; border-radius: 12px; padding: 30px 20px; display: flex; flex-direction: column; 
            justify-content: flex-end; text-decoration: none; overflow: hidden; transition: 0.4s ease; cursor: pointer; 
        }
        
        .app-card::after { 
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%; 
            background: linear-gradient(to top, rgba(5,5,5,0.95) 25%, rgba(5,5,5,0.5) 70%, rgba(5,5,5,0.2) 100%); z-index: 1; 
        }
        
        .app-card > * { position: relative; z-index: 2; }
        
        .app-card:hover { border-color: #ff4b2b; transform: translateY(-8px); box-shadow: 0 15px 30px rgba(255, 75, 43, 0.3); }
        
        .card-icon { font-size: 32px; margin-bottom: auto; color: #fff; }
        .card-content h3 { font-size: 14px; font-weight: 900; text-transform: uppercase; color: #fff; letter-spacing: 1.5px; }

        /* Form Layout */
        .form-wrapper { max-width: 700px; margin: 0 auto; background: #0e0e0e; border: 1px solid #222; border-radius: 12px; padding: 40px; box-shadow: 0 20px 40px rgba(0,0,0,0.6); }
        .form-wrapper h2 { font-size: 24px; text-transform: uppercase; margin-bottom: 8px; color: #fff; font-weight: 900; letter-spacing: 1px; }
        .form-wrapper p.desc { font-size: 12px; color: #888; text-transform: uppercase; margin-bottom: 25px; border-bottom: 2px solid #ff4b2b; padding-bottom: 10px; letter-spacing: 1px; font-weight: 600; }
        .input-group { margin-bottom: 20px; }
        label { display: block; font-size: 12px; font-weight: bold; text-transform: uppercase; margin-bottom: 8px; color: #ccc; letter-spacing: 1px; }
        input, select, textarea { width: 100%; padding: 14px; background: #151515; border: 1px solid #282828; border-radius: 6px; color: #fff; font-size: 14px; transition: 0.3s; }
        input:focus, select:focus, textarea:focus { border-color: #ff4b2b; outline: none; }
        textarea { resize: vertical; height: 110px; }
        .submit-btn { background: linear-gradient(90deg, #ff416c, #ff4b2b); color: white; border: none; padding: 15px; font-size: 14px; font-weight: bold; text-transform: uppercase; border-radius: 6px; cursor: pointer; width: 100%; transition: 0.3s; margin-top: 10px; letter-spacing: 1px; }
        .submit-btn:hover { opacity: 0.9; }
        .back-btn { display: inline-block; margin-top: 20px; color: #888; text-decoration: none; font-size: 12px; text-transform: uppercase; cursor: pointer; font-weight: bold; }
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
            <a onclick="showView('home')">Home</a>
            <a onclick="showView('whitelist')" style="color: #ff4b2b; font-weight: 900;">Blackout City Application</a>
            <a onclick="showView('home')">Rules</a>
            <a onclick="showView('home')">Team</a>
        </div>
    </nav>

    <div class="header-section">
        <h1>BLACKOUT CITY APPLICATIONS</h1>
        <p class="subtitle">Select a department to submit your official application directly to our team</p>
    </div>

    <!-- Home Section (Cards) -->
    <div id="home" class="page-view active">
        <div class="cards-container">
            <div class="app-card" onclick="showView('whitelist')" style="background-image: url('https://images.unsplash.com/photo-1506126613408-eca07ce68773?auto=format&fit=crop&w=500&q=80');">
                <div class="card-icon"></div>
                <div class="card-content">
                    <h3>Whitelist (Citizen)</h3>
                </div>
            </div>
            
            <div class="app-card" onclick="showView('gang')" style="background-image: url('https://images.unsplash.com/photo-1519085360753-af0119f7cbe7?auto=format&fit=crop&w=500&q=80');">
                <div class="card-icon"></div>
                <div class="card-content">
                    <h3>Gang & Family</h3>
                </div>
            </div>
            
            <div class="app-card" onclick="showView('police')" style="background-image: url('https://images.unsplash.com/photo-1589829545856-d10d557cf95f?auto=format&fit=crop&w=500&q=80');">
                <div class="card-icon"></div>
                <div class="card-content">
                    <h3>Police Department</h3>
                </div>
            </div>
            
            <div class="app-card" onclick="showView('ems')" style="background-image: url('https://images.unsplash.com/photo-1584515979956-d9f6e5d09982?auto=format&fit=crop&w=500&q=80');">
                <div class="card-icon"></div>
                <div class="card-content">
                    <h3>EMS Department</h3>
                </div>
            </div>
        </div>
    </div>

    <!-- Whitelist Form View -->
    <div id="whitelist" class="page-view">
        <div class="form-wrapper">
            <h2>Whitelist Application</h2>
            <p class="desc">Submit your citizenship request</p>
            <form onsubmit="alert('Submitted Successfully!'); return false;">
                <div class="input-group"><label>Real Name</label><input type="text" required></div>
                <div class="input-group"><label>Character Name</label><input type="text" required></div>
                <div class="input-group"><label>Age</label><input type="number" required></div>
                <div class="input-group"><label>Discord ID</label><input type="text" required></div>
                <div class="input-group"><label>Experience Level (1-10)</label><input type="number" min="1" max="10" required></div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('home')">&larr; Back to Home</a>
        </div>
    </div>

    <!-- Gang Form View -->
    <div id="gang" class="page-view">
        <div class="form-wrapper">
            <h2>Gang / Org Application</h2>
            <p class="desc">Register your organization</p>
            <form onsubmit="alert('Submitted Successfully!'); return false;">
                <div class="input-group"><label>Gang Name</label><input type="text" required></div>
                <div class="input-group"><label>Number of Members</label><input type="number" required></div>
                <div class="input-group"><label>Gang Backstory</label><textarea required></textarea></div>
                <div class="input-group"><label>Gang Goals</label><textarea required></textarea></div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('home')">&larr; Back to Home</a>
        </div>
    </div>

    <!-- Police Form View -->
    <div id="police" class="page-view">
        <div class="form-wrapper">
            <h2>Police Department Application</h2>
            <p class="desc">Enforce law and order</p>
            <form onsubmit="alert('Submitted Successfully!'); return false;">
                <div class="input-group"><label>Character Name</label><input type="text" required></div>
                <div class="input-group"><label>Why do you want to join the LSPD?</label><textarea required></textarea></div>
                <div class="input-group"><label>Have you ever been an officer before?</label><textarea required></textarea></div>
                <div class="input-group"><label>Availability (Hours/Week)</label><input type="text" required></div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('home')">&larr; Back to Home</a>
        </div>
    </div>

    <!-- EMS Form View -->
    <div id="ems" class="page-view">
        <div class="form-wrapper">
            <h2>EMS Department Application</h2>
            <p class="desc">Provide medical services</p>
            <form onsubmit="alert('Submitted Successfully!'); return false;">
                <div class="input-group"><label>Character Name</label><input type="text" required></div>
                <div class="input-group"><label>Why do you want to join EMS?</label><textarea required></textarea></div>
                <div class="input-group"><label>Medical Knowledge / Experience</label><textarea required></textarea></div>
                <div class="input-group"><label>Are you familiar with triage?</label>
                    <select><option>Yes</option><option>No</option></select>
                </div>
                <button type="submit" class="submit-btn">Submit Application</button>
            </form>
            <a class="back-btn" onclick="showView('home')">&larr; Back to Home</a>
        </div>
    </div>

    <script>
        function showView(viewId) {
            document.querySelectorAll('.page-view').forEach(v => v.classList.remove('active'));
            document.getElementById(viewId).classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
    </script>
</body>
</html>
