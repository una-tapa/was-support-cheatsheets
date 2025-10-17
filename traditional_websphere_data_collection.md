# 🧩 WebSphere Manual Data Collection Checklist (Core Security Issue)

<details>
<summary><b>1️⃣ Preparation</b></summary>

- Answer diagnostic questions:
  - What action triggered the problem?
  - Can it be reproduced? If yes, list exact steps.
  - Which JVMs are affected (dmgr, nodeagent, server1, cluster members)?
  - Timestamp of the issue and related logs (SystemOut.log).
  - Any troubleshooting steps already tried?

</details>

<details>
<summary><b>2️⃣ Enable Core Security Trace</b></summary>

**If Admin Console is available:**
1. Go to **Troubleshooting → Logs and Trace → _server_name_ → Diagnostic trace service**
2. Under **Trace Output**, select **File**
3. Set **Max File Size ≥ 20 MB** and **Max Historical Files ≥ 20**
4. Click **Apply**
5. Click **Change log level details** → Clear existing → Enter:
   ```
   *=info:com.ibm.ws.security.*=all:com.ibm.websphere.security.*=all:
   com.ibm.websphere.wim.*=all:com.ibm.wsspi.wim.*=all:com.ibm.ws.wim.*=all
   ```
   - If EJB/auth issue → append `:SASRas=all:ORBRas=all`
   - If security domains issue → append `:SecurityDomain=all`
6. Click **Apply → Save**

**If Admin Console not available:**  
Use the “start/stop problems” MustGather instructions to set the same trace spec manually.

</details>

<details>
<summary><b>3️⃣ Optional: Enable COMM Trace (only if IBM requests)</b></summary>

Add to Generic JVM Arguments:
```
-Dcom.ibm.CORBA.Debug=true
-Dcom.ibm.CORBA.CommTrace=true
```

</details>

<details>
<summary><b>4️⃣ Capture Trace Data</b></summary>

For each traced JVM:
1. Stop the server
2. Back up & clear `logs` and `FFDC` directories
3. Start the server
4. Reproduce the issue
5. Record exact timestamp of the problem

</details>

<details>
<summary><b>5️⃣ Gather Files for IBM Support</b></summary>

- Diagnostic answers (Step 1)
- Collector tool output from each `<PROFILE_ROOT>`:
  ```
  <PROFILE_ROOT>/bin/collector.sh   (Linux/Unix)
  <PROFILE_ROOT>\bin\collector.bat  (Windows)
  ```
  *(Ignore any “deprecated” message)*
- If multiple security domains → include all under:
  ```
  <PROFILE_ROOT>/config/waspolicies
  ```
- All related logs/traces covering the issue window

</details>

<details>
<summary><b>6️⃣ Wrap Up</b></summary>

- Disable tracing and restore normal log settings
- Send all collected files using the “Exchanging information with IBM Technical Support” procedure

</details>
