<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aland Wasim</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <link rel="icon" href="https://a.deviantart.net/avatars-big/a/l/aland1w.jpg?2" type="image/png">
    <style>
        * {
            box-sizing: border-box;
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            transition: all 0.3s ease;
        }

        :root {
            --bg-primary: #1e1e2f;
            --bg-secondary: #2a2a3d;
            --text-primary: #ffffff;
            --text-secondary: #999;
            --accent-color: #3ba3db;
            --input-bg: #333;
            --input-border: #444;
            --table-border: #444;
        }

        [data-theme="light"] {
            --bg-primary: #f0f2f5;
            --bg-secondary: #ffffff;
            --text-primary: #333333;
            --text-secondary: #666666;
            --accent-color: #2196f3;
            --input-bg: #ffffff;
            --input-border: #dddddd;
            --table-border: #e0e0e0;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: var(--bg-primary);
            color: var(--text-primary);
        }

        .container {
            background-color: var(--bg-secondary);
            border-radius: 10px;
            width: 90%;
            max-width: 800px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin: 20px 0;
        }

        .header {
            text-align: center;
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 20px;
            color: var(--accent-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .theme-toggle {
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            background: var(--input-bg);
            border: 1px solid var(--input-border);
            color: var(--text-primary);
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            font-size: 1em;
            color: var(--text-secondary);
        }

        input[type="text"] {
            width: 100%;
            padding: 10px;
            border: 1px solid var(--input-border);
            border-radius: 5px;
            background-color: var(--input-bg);
            color: var(--text-primary);
            outline: none;
            font-size: 0.9em;
        }

        input[type="text"]:focus {
            border-color: var(--accent-color);
        }

        .btn {
            width: 100%;
            padding: 10px;
            background-color: var(--accent-color);
            border: none;
            border-radius: 5px;
            color: #fff;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            margin-bottom: 10px;
        }

        .btn:hover {
            opacity: 0.9;
        }

        .result {
            margin-top: 15px;
            padding: 15px;
            background-color: var(--input-bg);
            border-radius: 5px;
            color: var(--text-primary);
            font-size: 0.9em;
        }

        .subnet-table {
            display: none;
            margin-top: 20px;
            width: 100%;
            background-color: var(--input-bg);
            border-radius: 5px;
            max-height: 400px;
            overflow-y: auto;
        }

        .subnet-table::-webkit-scrollbar {
            width: 8px;
        }

        .subnet-table::-webkit-scrollbar-track {
            background: var(--bg-secondary);
            border-radius: 4px;
        }

        .subnet-table::-webkit-scrollbar-thumb {
            background: var(--accent-color);
            border-radius: 4px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            position: relative;
        }

        thead {
            position: sticky;
            top: 0;
            z-index: 1;
        }

        table, th, td {
            border: 1px solid var(--table-border);
        }

        th, td {
            padding: 12px;
            text-align: center;
            color: var(--text-primary);
            font-size: 0.9em;
        }

        th {
            background-color: var(--accent-color);
            color: #ffffff;
            font-weight: bold;
        }

        tr:nth-child(even) {
            background-color: var(--bg-primary);
        }

        .alert {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background-color: var(--bg-secondary);
            color: #ff4444;
            padding: 12px 24px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            z-index: 1000;
            border: 1px solid #ff4444;
            display: none;
            animation: fadeIn 0.3s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translate(-50%, -20px); }
            to { opacity: 1; transform: translate(-50%, 0); }
        }

        @media (max-width: 500px) {
            .container {
                padding: 15px;
                width: 95%;
            }

            .header {
                font-size: 1.2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">

        
        <div class="header">
            <span>Network IP & Subnet Calculator</span>
            <button class="theme-toggle" onclick="toggleTheme()">
                <i class="fas fa-sun"></i>
            </button>
        </div>
        <div class="form-group">
            <label for="ipAddress">Enter IP Address:</label>
            <input type="text" id="ipAddress" placeholder="e.g., 192.168.1.1">
        </div>
        <div class="form-group">
            <label for="subnetMask">Enter Subnet Mask:</label>
            <input type="text" id="subnetMask" placeholder="e.g., 255.255.255.0 or /24">
        </div>
        <div class="alert" id="numberAlert">Please enter numbers only</div>
        <button class="btn" onclick="calculateSubnet()">Calculate</button>
        <div class="result" id="result"></div>
        <div class="subnet-table" id="subnetTable"></div>
        <br />

        <div style="background-color: var(--bg-primary); padding: 15px; border-radius: 8px; margin-bottom: 20px; border: 1px solid var(--input-border);  text-align: center;">
            <h3 style="color: var(--accent-color); margin-bottom: 10px;">Network Class Ranges:</h3>
            <p style="color: var(--text-secondary); font-size: 0.9em; margin-bottom: 5px;">Class A: 1.0.0.0 to 126.255.255.255</p>
            <p style="color: var(--text-secondary); font-size: 0.9em; margin-bottom: 5px;">Loop Back: 127.0.0.0 to 127.255.255.255</p>
            <p style="color: var(--text-secondary); font-size: 0.9em; margin-bottom: 5px;">Class B: 128.0.0.0 to 191.255.255.255</p>
            <p style="color: var(--text-secondary); font-size: 0.9em; margin-bottom: 5px;">Class C: 192.0.0.0 to 223.255.255.255</p>
            <br>
            <p style="color: var(--accent-color); margin-bottom: 8px;">Private IP Ranges:</p>
            <p style="color: var(--text-secondary); font-size: 0.9em; margin-bottom: 5px;">(Class A) : 10.0.0.0 to 10.255.255.255 </p>
            <p style="color: var(--text-secondary); font-size: 0.9em; margin-bottom: 5px;">(Class B) : 172.16.0.0 to 172.31.255.255 </p>
            <p style="color: var(--text-secondary); font-size: 0.9em;">(Class C) : 192.168.0.0 to 192.168.255.255 </p>
     
        </div>
        <footer style="text-align: center; margin-top: 20px; font-size: 14px; color: #666;">
            <p><strong><a href="https://t.me/AW_Graphic_IT" style="color: #0088cc; text-decoration: none;">Aland</a></strong>   2024© </p>
        </footer>
        
    </div>

    
    <script>
        // Theme management
        function toggleTheme() {
            const body = document.body;
            const themeToggle = document.querySelector('.theme-toggle i');
            const currentTheme = body.getAttribute('data-theme');
            
            if (currentTheme === 'light') {
                body.removeAttribute('data-theme');
                themeToggle.classList.remove('fa-moon');
                themeToggle.classList.add('fa-sun');
            } else {
                body.setAttribute('data-theme', 'light');
                themeToggle.classList.remove('fa-sun');
                themeToggle.classList.add('fa-moon');
            }
        }

        

        function showNumberAlert() {
            const alert = document.getElementById('numberAlert');
            alert.style.display = 'block';
            
            setTimeout(() => {
                alert.style.display = 'none';
            }, 4000);
        }
        
        // Modify the input event listeners for both fields
        document.getElementById('ipAddress').addEventListener('input', function(e) {
            if (!/^\d*\.?\d*\.?\d*\.?\d*$/.test(this.value)) {
                this.value = this.value.replace(/[^\d.]/g, '');
                showNumberAlert();
            }
        });
        
        document.getElementById('subnetMask').addEventListener('input', function(e) {
            if (!/^(\d*\.?\d*\.?\d*\.?\d*|\/?\d*)$/.test(this.value)) {
                this.value = this.value.replace(/[^\d./]/g, '');
                showNumberAlert();
            }
        });

        function calculateSubnet() {
            const ipAddress = document.getElementById('ipAddress').value;
            const subnetMask = document.getElementById('subnetMask').value;
            const result = document.getElementById('result');
            const subnetTable = document.getElementById('subnetTable');

            const isValidIP = ipAddress.match(/^(\d{1,3}\.){3}\d{1,3}$/);
            if (!isValidIP) {
                result.innerHTML = "Please enter a valid IP address.";
                subnetTable.style.display = "none";
                return;
            }

            function determineIPClass(ip) {
                const firstOctet = parseInt(ip.split('.')[0]);
                
                if (firstOctet >= 1 && firstOctet <= 126) {
                    return { class: 'A', type: firstOctet === 10 ? 'Private' : 'Public' };
                } else if (firstOctet === 127) {
                    return { class: 'Loopback', type: 'Reserved' };
                } else if (firstOctet >= 128 && firstOctet <= 191) {
                    const secondOctet = parseInt(ip.split('.')[1]);
                    return { 
                        class: 'B', 
                        type: (firstOctet === 172 && secondOctet >= 16 && secondOctet <= 31) ? 'Private' : 'Public'
                    };
                } else if (firstOctet >= 192 && firstOctet <= 223) {
                    const secondOctet = parseInt(ip.split('.')[1]);
                    return { 
                        class: 'C', 
                        type: (firstOctet === 192 && secondOctet === 168) ? 'Private' : 'Public'
                    };
                } else if (firstOctet >= 224 && firstOctet <= 239) {
                    return { class: 'D', type: 'Multicast' };
                } else if (firstOctet >= 240 && firstOctet <= 255) {
                    return { class: 'E', type: 'Reserved' };
                }
                return { class: 'Invalid', type: 'Invalid' };
            }

            let maskBinary = "";
            let cidr = 0;

            if (subnetMask.includes('/')) {
                cidr = parseInt(subnetMask.slice(1));
                if (cidr < 1 || cidr > 32) {
                    result.innerHTML = "CIDR notation must be between /1 and /32.";
                    subnetTable.style.display = "none";
                    return;
                }
                maskBinary = "1".repeat(cidr).padEnd(32, "0");
            } else if (subnetMask.match(/^(\d{1,3}\.){3}\d{1,3}$/)) {
                maskBinary = subnetMask.split('.')
                    .map(num => parseInt(num).toString(2).padStart(8, '0'))
                    .join('');
                cidr = maskBinary.replace(/0/g, '').length;
            } else {
                result.innerHTML = "Please enter a valid subnet mask (e.g., 255.255.255.0 or /24).";
                subnetTable.style.display = "none";
                return;
            }

            const ipBinary = ipAddress.split('.').map(num => parseInt(num).toString(2).padStart(8, '0')).join('');
            const networkBinary = ipBinary.slice(0, cidr) + "0".repeat(32 - cidr);
            const broadcastBinary = ipBinary.slice(0, cidr) + "1".repeat(32 - cidr);

            const networkAddress = parseBinaryToIP(networkBinary);
            const broadcastAddress = parseBinaryToIP(broadcastBinary);
            const defaultCIDR = getDefaultCIDR(ipAddress);
            const bitsBorrowed = cidr - defaultCIDR;
            const totalSubnets = Math.pow(2, bitsBorrowed);
            const totalHosts = Math.pow(2, 32 - cidr);
            const usableHosts = totalHosts - 2;

            const ipClass = determineIPClass(ipAddress);
result.innerHTML = `
    <strong>IP Class:</strong> Class ${ipClass.class} (${ipClass.type})<br>
    <strong>Network Address:</strong> ${networkAddress}<br>
    <strong>Broadcast Address:</strong> ${broadcastAddress}<br>
    <strong>Subnet Mask (Binary):</strong> ${maskBinary.match(/.{8}/g).join('.')}<br>
    <strong>CIDR Notation:</strong> /${cidr}<br>
    <strong>Bits Borrowed:</strong> ${bitsBorrowed}<br>
    <strong>Total Subnets:</strong> ${totalSubnets}<br>
    <strong>Total Hosts per Subnet:</strong> ${totalHosts}<br>
    <strong>Usable Hosts per Subnet:</strong> ${usableHosts}<br>
`;

            subnetTable.style.display = "block";
            generateSubnetRows(networkBinary, cidr, totalSubnets);
        }

        function parseBinaryToIP(binary) {
            return binary.match(/.{8}/g).map(b => parseInt(b, 2)).join('.');
        }

        function getDefaultCIDR(ip) {
            const firstByte = parseInt(ip.split('.')[0]);
            if (firstByte < 128) return 8;
            if (firstByte < 192) return 16;
            return 24;
        }

        function generateSubnetRows(networkBinary, cidr, totalSubnets) {
            const subnetTable = document.getElementById('subnetTable');
            subnetTable.innerHTML = `
                <table>
                    <thead>
                        <tr>
                            <th>Subnet</th>
                            <th>Network</th>
                            <th>Host Range</th>
                            <th>Broadcast</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            `;
            const tbody = subnetTable.querySelector('tbody');
            const increment = Math.pow(2, 32 - cidr);
            
            for (let i = 0; i < totalSubnets; i++) {
                const subnetNetworkBinary = (parseInt(networkBinary, 2) + i * increment).toString(2).padStart(32, '0');
                const subnetBroadcastBinary = (parseInt(subnetNetworkBinary, 2) + increment - 1).toString(2).padStart(32, '0');

                const networkAddress = parseBinaryToIP(subnetNetworkBinary);
                const broadcastAddress = parseBinaryToIP(subnetBroadcastBinary);
                const firstHost = parseBinaryToIP((parseInt(subnetNetworkBinary, 2) + 1).toString(2).padStart(32, '0'));
                const lastHost = parseBinaryToIP((parseInt(subnetBroadcastBinary, 2) - 1).toString(2).padStart(32, '0'));

                const row = tbody.insertRow();
                row.insertCell(0).innerText = i + 1;
                row.insertCell(1).innerText = networkAddress;
                row.insertCell(2).innerText = `${firstHost} - ${lastHost}`;
                row.insertCell(3).innerText = broadcastAddress;
            }
        }
    </script>
</body>
</html>
