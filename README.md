<html>
<head>
     <title>[CHALCENTRON_137 TERMINAL_INTERFACE]</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
   
    <style>
    /* Absolute Style Reset to Kill GitHub Themes */
    html, body, div, span, input {
        margin: 0 !important;
        padding: 0 !important;
        border: none !important;
        outline: none !important;
        background-color: #030303 !important;
        box-shadow: none !important;
    }

    /* Force 14pt Courier Prime Matrix Styling */
    body {
        background-color: #030303 !important;
        color: #00cc44 !important;
        font-family: 'Courier Prime', 'Courier New', Courier, monospace !important;
        font-size: 14pt !important;
        line-height: 1.5 !important;
        padding: 40px !important; /* Re-inject internal spacing safely */
        overflow-x: hidden;
    }

    /* Target the text input directly to prevent font fallback glitches */
    #cmd-input {
        background: transparent !important;
        border: none !important;
        color: #00cc44 !important;
        font-family: 'Courier Prime', 'Courier New', Courier, monospace !important;
        font-size: 14pt !important;
        flex-grow: 1;
        outline: none !important;
    }

    /* Scanline Effect Overlay */
    body::before {
        content: " ";
        display: block;
        position: fixed;
        top: 0; left: 0; bottom: 0; right: 0;
        background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%);
        z-index: 99999;
        background-size: 100% 3px;
        pointer-events: none;
    }

    #terminal {
        max-width: 900px;
        margin: 0 auto;
    }

    .output-line {
        white-space: pre-wrap;
        margin-bottom: 6px;
    }

    #input-container {
        display: flex;
        align-items: center;
        margin-top: 15px;
    }

    #prompt {
        margin-right: 10px;
        font-weight: bold;
        user-select: none;
    }
</style>

</head>
<body>

<div id="terminal">
    <div id="output">
        <div class="output-line">
===================================================================</div>
        <div class="output-line">[CHALCENTRON_137 INITIALIZATION PROTOCOL]</div>
        <div class="output-line">SECTOR CALIBRATION: [26] [DATA INTEGRITY: SEALED]
INTERFACE STATUS: [BEGIN_EXECUTION]</div><div class="output-line">
===================================================================</div>
        <div class="output-line">Type <span style="text-decoration: underline;">HELP</span> to view a list of available system subroutines.</div>
        <div class="output-line"></div>
    </div>
    
    <div id="input-container">
        <span id="prompt">C:\&gt;</span>
        <input type="text" id="cmd-input" autofocus autocomplete="off" spellcheck="false">
    </div>
</div>

<script>
    const outputDiv = document.getElementById('output');
    const cmdInput = document.getElementById('cmd-input');

    // System Log Database
    const logLibrary = {
        "infraction_01": `[LORE LOG: INFRACTION 01 // THE CHRONOPHAGE]
-------------------------------------------------------------------
* Tumor: [THAUMIEL] (The Split Crown)
* Inborn Matter: Crystallized, hyper-conductive copper soot.
* Diagnostic: A temporal parasite perceiving un-rendered cycles.
* Script: Hardcoded to panic and warn cells. Its unchangeable fate 
  is to be flushed from volatile memory and re-indexed.`,
        
        "infraction_04": `[LORE LOG: INFRACTION 04 // THE PHONOPHAGE]
-------------------------------------------------------------------
* Tumor: [A'ARAB ZARAQ] (The Desolation of Splendor)
* Inborn Matter: Porous, acoustic lattice of brass alloy.
* Diagnostic: Detects the exact moment reality cuts audio tracks to 
  patch itself, isolating the breathing of the void.
* Script: Hardcoded to lock itself away in search of silence.`,

        "infraction_10": `[LORE LOG: INFRACTION 10 // SOUL-SEPSIS]
-------------------------------------------------------------------
* Tumor: [GAMALIEL] (The Obscene Foundation)
* Inborn Matter: Glowing subcutaneous copper capillaries.
* Diagnostic: Pumps infected, recycled soul-matter back into loops.
* Script: Neonatal nurse feeding raw static infants. Stands wide 
  awake screaming inside a smiling, automated flesh suit.`
    };

    // Keep input focused even if user clicks elsewhere
    document.addEventListener('click', () => cmdInput.focus());

    cmdInput.addEventListener('keydown', function(e) {
        if (e.key === 'Enter') {
            const rawInput = this.value;
            const cleanInput = rawInput.trim().toLowerCase();
            this.value = '';

            // Echo the command back to screen
            printLine(`C:\\> ${rawInput}`);

            if (cleanInput !== '') {
                executeCommand(cleanInput);
            }
        }
    });

    function printLine(text, isDim = false) {
        const line = document.createElement('div');
        line.className = 'output-line' + (isDim ? ' dim' : '');
        line.textContent = text;
        outputDiv.appendChild(line);
        window.scrollTo(0, document.body.scrollHeight);
    }

    function executeCommand(cmd) {
        const args = cmd.split(' ');
        const primaryCmd = args[0];

        switch(primaryCmd) {
            case 'help':
                printLine(`\n[AVAILABLE SYSTEM ROUTINES]:`);
                printLine(`  HELP        - Displays this navigation tree.`);
                printLine(`  DIR         - Lists executable files and system directories.`);
                printLine(`  SYS_DIAG    - Executes automated system homeostasis check.`);
                printLine(`  TYPE [log]  - Reads contents of a specific file (e.g., TYPE INFRACTION_01)`);
                printLine(`  RUN [exe]   - Executes trap-contingency files.`);
                printLine(`  CLS         - Clears the active terminal output memory.\n`);
                break;

            case 'dir':
                printLine(`\n Directory of C:\\CHALCENTRON_137\\LOGS\n`);
                printLine(`06/02/2026  01:47 PM    <DIR>          .`);
                printLine(`06/02/2026  01:47 PM    <DIR>          ..`);
                printLine(`06/02/2026  01:47 PM             1,024 INFRACTION_01.LOG`);
                printLine(`06/02/2026  01:47 PM             1,024 INFRACTION_04.LOG`);
                printLine(`06/02/2026  01:47 PM             1,024 INFRACTION_10.LOG`);
                printLine(`06/02/2026  01:47 PM             4,096 ESCAPE_ROUTINE.EXE`);
                printLine(`               4 File(s)          7,168 bytes\n`);
                break;

            case 'cls':
                outputDiv.innerHTML = '';
                break;

            case 'sys_diag':
                printLine(`\n[INITIALIZING AUTOMATED HOMEOSTASIS SWEEP...]`);
                setTimeout(() => printLine(`Sectors Checked: [26] / Status: [STABLE]`), 200);
                setTimeout(() => printLine(`Homeostasis Index: [100.00%]`), 400);
                setTimeout(() => printLine(`Quarantined Anomalies: [1] / [1]`), 600);
                setTimeout(() => {
                    printLine(`\n[CRITICAL NOTICE]: Lingerer Pathogen detected reading terminal records.`);
                    printLine(`Target coordinates locked via copper pathway alignments.`);
                    printLine(`SYSTEM STATUS: OPTIMIZED. BALANCED AT [1:1].\n`);
                }, 900);
                break;

            case 'type':
                if (!args[1]) {
                    printLine(`Error: Command requires a file parameter. Example: TYPE INFRACTION_01.LOG`);
                } else {
                    const targetFile = args[1].replace('.log', '');
                    if (logLibrary[targetFile]) {
                        printLine(`\n${logLibrary[targetFile]}\n`);
                    } else {
                        printLine(`Error: File [${args[1].toUpperCase()}] not found in localized directory.`);
                    }
                }
                break;

            case 'run':
                if (!args[1]) {
                    printLine(`Error: Command requires an executable parameter. Example: RUN ESCAPE_ROUTINE.EXE`);
                } else {
                    const targetExe = args[1].replace('.exe', '');
                    if (targetExe === 'escape_routine') {
                        printLine(`\nExecuting: ESCAPE_ROUTINE.EXE...`);
                        setTimeout(() => printLine(`[Error 404]: Destination invalid.`), 300);
                        setTimeout(() => printLine(`All paths lead inward. Every desperate alignment is a system asset.`), 600);
                        setTimeout(() => {
                            printLine(`You cannot weaponize the machine against the machine.`);
                            printLine(`THE TERMINAL YOU ARE TYPING ON IS CHALCENTRON_137.\n`);
                        }, 900);
                    } else {
                        printLine(`Error: Executable [${args[1].toUpperCase()}] is corrupted or missing signature.`);
                    }
                }
                break;

            default:
                printLine(`Bad command or file name: '${cmd}'. Type HELP for diagnostic list.`);
        }
    }
</script>

</body>
</html>




