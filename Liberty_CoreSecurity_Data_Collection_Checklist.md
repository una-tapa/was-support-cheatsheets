# 🧩 Liberty Manual Data Collection Checklist (Core Security Issue)

<details>
<summary><b>1️⃣ Set Up Liberty for Core Security Tracing</b></summary>

1. Follow the steps in **“Enabling Trace on Liberty”** from *Set up trace and get a full dump for WebSphere Liberty*.
2. Use the following trace specification:
   ```
   com.ibm.ws.security.*=all:com.ibm.ws.webcontainer.security.*=all
   ```
3. For more details, refer to *Liberty: Logging and Trace* in IBM Documentation.

**Verify that tracing is active:**
1. Stop the Liberty server.
2. Delete existing log files under:
   ```
   <LIBERTY_HOME>/usr/servers/<serverName>/logs
   ```
3. Restart the server and ensure the logs are new.
4. Confirm that the new trace setting is applied by checking the top of `trace.log`.

</details>

<details>
<summary><b>2️⃣ Collect Liberty Core Security Traces</b></summary>

⚠️ Core security traces must be captured **from Liberty server startup**.

1. Stop the Liberty server.
2. Restart the Liberty server.
3. Reproduce the problem.
4. Record useful details, such as:
   - Relevant user and group names
   - Exact URL strings accessed
   - Approximate timestamps

</details>

<details>
<summary><b>3️⃣ Gather Liberty Data to Send to IBM Support</b></summary>

**Generate dump ZIP (logs + configs):**

- **Windows**
  ```
  <LIBERTY_HOME>\bin\server.bat dump <serverName>
  ```
- **UNIX/Linux**
  ```
  <LIBERTY_HOME>/bin/server dump <serverName>
  ```

The resulting file (for example:  
`myserver.dump-17.03.20_22.20.57.zip`) will be created under:
```
<LIBERTY_HOME>/usr/servers/<serverName>/
```

**Also collect:**
```
<JAVA_HOME>/lib/security/java.security
```

✅ Ensure the trace covers the timeframe of the issue.

When ready, send the `.zip` and supplemental information following  
**“Exchanging information with IBM Technical Support for problem determination.”**

</details>
