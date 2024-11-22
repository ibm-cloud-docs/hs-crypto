# Agent messages

The following list describes the messages that are issued by the {{site.data.keyword.uko_short}} Agent. The messages are written to the SYSOUT DD name for the started task. Selected messages are also written to the system log as WTO messages, usable for automated operation. The WTO messages are issued with routing codes 2, 9 and 11.

The message number followed by 'I' signifies an informational message, 'E' signifies an error message and 'W' signifies a warning message.

| Message ID | Message | Description | 
|-----|-----|-----|
| KMG001I | {{site.data.keyword.ekmf_short}} Agent initialization has completed. | This is a WTO message.<br> When this message is issued, the initialization of the Agent started task is completed. |
| KMG002E | {{site.data.keyword.ekmf_short}} Agent abnormal termination. | This is a WTO message.<br> This message is issued when an error has occurred during initialization of the Agent started task, or an unrecoverable error has occurred after initialization. Other messages may be issued describing the actual error. Inspect the system log and the SYSOUT for the Agent started task to retrieve additional information. |
| KMG003E | Failure to access TSSPARAM Db2 table.<br>SQL Code: xx. SQLCA Data Structure: xxxxxx. | The SQL error code is described in the manual 'Messages and codes' for DB2.<br> Typical errors are bind errors and access to the Db2 plan/package errors. |
| KMG004I | {{site.data.keyword.ekmf_short}} Agent termination due to DB2 termination. | This is an expected message when Db2 stops. Restart the Agent again when Db2 is available. |
| KMG007E | TCP/IP Error. Socket Function: xxxxxx. Socket Error: xx. | The socket function is the sub-function to the z/OS TCP/IP callable service EZASOKET. A description of the socket error (xx) can be found in the [Sockets return codes documentation of the z/OS Communications Server](https://www.ibm.com/docs/en/zos/3.1.0?topic=errnos-sockets-return-codes). The socket error corresponds to the error number (errno) from the documentation. The socket error '48', address and TCP/IP port in use, may occur when the Agent is stopped and started within a short interval (0 - 15 seconds). Wait some seconds before restarting the task. |
| KMG008W | TCP/IP Time-out on reading data from client. | An incomplete request has been received from a client. This message will, for example, occur if a client is sending data to the Agent, but is not using the EKMF proprietary communication protocol correctly. This message can indicate an unauthorized attempt to access the Agent. |
| KMG009W | TCP/IP Connection closed by client. | Could be the {{site.data.keyword.uko_short}} client abruptly ending, or some network layer stopping the connection. |
| KMG010W | Invalid transaction - Length not numeric. | This message will, for example, occur if a client is sending data to the Agent, but is not using the EKMF proprietary communication protocol correctly. This message could indicate an unauthorized attempt to access the Agent. |
| KMG011W | Length too short/long. Length: xxxx | A request from a client is received. The length of the request is either too short or too long for the EKMF proprietary communication protocol.<br> This message could indicate an unauthorized attempt to access the host. |
| KMG012W | TCP/IP Time-out on reading data from client. | An incomplete request has been received from a client. This message will, for example, occur if a client sends data to the Agent; but is not using the EKMF proprietary communication protocol, or a {{site.data.keyword.uko_short}} client has abruptly ended.<br> This message could indicate an unauthorized attempt to access the host. |
| KMG013W | TCP/IP connection closed by client. | Could be the {{site.data.keyword.uko_short}} client abruptly ending, or some network layer stopping the connection. |
| KMG014W | Time-out during sending data to the client. | It was not possible for the Agent to reply to a request from a client. |
| KMG015E | Failed to access the ICSF - CSFIQF function failed. Return code: xx Reason code: yy. | The return code and reason code can be found in the ICSF Application Programmer's Guide, Appendix A. |
| KMG018I | {{site.data.keyword.ekmf_short}} Agent terminated by command. | This is a WTO message.<br> The started task has been purged, or canceled, or stopped upon request from the operator command. |
| KMG019W | Link Encryption is not required. | This message indicates that the SAF FACILITY resource KMG.EKMF.LNKCRYOFF is permitted to the Agent user ID. <br>The current status of the link encryption between the {{site.data.keyword.uko_short}} client and the Agent is not required and is not determined by the {{site.data.keyword.uko_short}} client.<br> See also the message KMG020I. |
| KMG020I | Link encryption is required. | Link encryption between the EKMF Workstation and the Agent is required. The {{site.data.keyword.uko_short}} client user cannot connect to the Agent without link encryption.<br> See also the message KMG019W. |
| KMG021E | Failed to open KMGPARM DD. Return code: xx. | The Agent failed to open the options data set. The return code specifies the I/O return code for the Open command. |
| KMG022E | Failed to read from KMGPARM DD. Return code: xx. | The Agent to read from the option data set. The return code specifies the<br>I/O return code for the read command |
| KMG023W | Audit is not enforced. | The Agent user ID is permitted to FACILITY resource KMG.EKMF.AUDITOFF. If the {{site.data.keyword.uko_short}} client user ID is also permitted, then the client user can disable logging to SMF for {{site.data.keyword.uko_short}} events. |
| KMG024I | Audit is enforced. | The Agent user ID is NOT permitted to FACILITY resource KMG.EKMF.AUDITOFF. The {{site.data.keyword.uko_short}} client user ID cannot disable logging to SMF for {{site.data.keyword.uko_short}} events. |
| KMG025E | AUDITOFF query returned unexpected: error-type, RACF rc, RACF rs. | | 
| KMG050E | KMGPRACF auth. Program not found in an auth library.<br> The APF KMGPRACF authorized program not found in an authorized library. | This is a WTO message. Ensure you performed the required [APF authorization steps](install-agent.md#apf-authorization) |
| KMG051E | APF auth program KMGPRACF was invoked from non TSO/E. <br>The APF authorized program KMGPRACF was invoked from a nonTSO/E environment.  | This is a WTO message. |
| KMG052E | Failed to call the APF authorized module KMGPRACF. | This is a WTO message.<br> See KMG053E as well. |
| KMG053E | Error from TSO/E service facility routine TSOLNK/IKJEFTSR. Error type: 36 return code yy. |  The return code yy can be found in the manual TSO/E Programming Services for the TSO/E service facility IKJEFTSR. |
| KMG054E | Error from RACF/Security server. RACF return code : xx. |  The return code xx can be found in the RACF Messages and Codes.<br> For return code 8 it will additionally display:<br>Access to the resource not permitted to task user. Resource KMG.EKMF.KMGPRACF.              |
| KMG055E | The module KMGPRACF is not running authorized. | Check SYS1.PARMLIB(IKJTSOxx) or similar data set for registration of the APF authorized program. The table AUTHTSF must specify the KMGPRACF module. A refresh of the table is required whenever this table is changed. If the module name is present in the table, refresh may not have been performed yet. |
| KMG057E | The TCP/IP network is down. | Try to start the Agent again when the network is up. |
| KMG058E | The TCP/IP port is in use. Port: &lt;port&gt; | Try to start the Agent again after a short while. Another task is using the port, or the port is not yet released by TCP/IP from a former instance of the Agent.  |
| KMG101I | CSFCRC ICSF refresh OK for CKDS/PKDS | This is a WTO message. |
| KMG102E | CSFCRC ICSF refresh failed for CKDS/PKDS – return-code, reason-code | This is a WTO message. |
| KMG201E | TSOLNK-KMGPRACF Error. A=XX,B=YY,C=ZZ. |  An error is returned from the TSOLNK module.<br> The XX code retrieved from the TSOLNK parameter 4, the YY code is retrieved from<br>TSOLNK parameter 5, and the ZZ code is retrieved from parameter 6.<br> The return code XX, YY and ZZ can be found in the manual TSO/E Programming Services for the TSO/E service facility IKJEFTSR. |
| KMG240I | {{site.data.keyword.ekmf_short}} Agent console interface ready | The Agent is now ready to receive modify and stop commands from the MVS console. |
| KMG250I | ICSF FMID FROM CCVT : CCVTID/VER: xxxxxx CCVTFMID: HCRxxxx | | 
| KMG251I | TCP/IP host name is &lt;host name&gt; | | 
| KMG252E | Fail to retrieve ICSF CCVT information. <br>TYPE=&lt;RACF-ERROR-TYPE&gt;<br> RC=&lt;RACF-RETURN-CODE&gt;<br>RE=&lt;RACF-REASON-CODE&gt;| | 
| KMG253I | No key hierarchy letter in the database SQLCODE = &lt;sqlcode&gt; | Select PTSS_TEST_MODE from view VTSSPARAM where PTSS_BFC_NO = '00'.<br> When not set, the SQLCODE will be 100.<br>It is perfectly valid not to have a key hierarchy letter defined in the database, however, some features require it. |
| KMG254I | Key hierarchy letter = &lt;key hierarchy letter&gt; | Select PTSS_TEST_MODE from view VTSSPARAM where PTSS_BFC_NO = '00' |
| KMG255E | SQLCODE = &lt;rc&gt; getting plan qualifier | Module KMGPQIBM needs to be bound to the Db2 plan to get the qualifier from SYSIBM.SYSPLAN.<br>Consider using the KMGPARM option &amp;DB2-QUALIFIER instead, if the problem persists.<br>Restart the Agent when either the &amp;DB2-QUALIFIER is been specified or KMGPQIBM successfully retrieves the qualifier from the Db2 plan.  |
| KMG0256I | Plan qualifier = &lt;qualifier or schema&gt; | This is the table and view qualifier by which the {{site.data.keyword.uko_short}} database tabels and views are found. |
| KMG257E | Plan qualifier and creator is 0 or &gt;24 chars. | Use a qualifier with a maximum of 24 characters for the {{site.data.keyword.uko_short}} database tables and views<br>Restart the Agent when either the &amp;DB2-QUALIFIER is been specified or KMGPQIBM successfully retrieves the qualifier from the Db2 plan. |
| KMG258E | KMGPARM OPTION(S) FOR JDBC MISSING | When &amp;DB2-USE(YES) is specified then the Agent must be configured with:<br>- &amp;SYS-JDBC-LOCATION<br>- &amp;SYS-JDBC-PORT and/or &amp;SYS-JDBC-SECPORT<br>- &amp;DB2-QUALIFIER or qualifier extracted through the plan using KMGPQIBM<br>Restart the Agent when above is corrected. |
| KMG259E | Error getting enhanced wrapping status.<br>- RETURN-CODE = &lt;rc&gt;<br>- REASON-CODE = &lt;rs&gt; |
| KMG260I | KMG-LEVEL=&lt;xxxxxx&gt; &lt;change-date&gt; &lt;FMID&gt;.<br>&lt;xxxxxx&gt; = KMG level of code in use, the level of KMGPTRAN.<br>&lt;change-date&gt; = The date KMGTRAN was changed.<br>&lt;FMID&gt; = the current FMID. |
| KMG261I |   SYSINFO:         <br> - ZOS REL &lt;vvrrmm&gt;       <br> - Z SERIAL &lt;serial&gt; <br> - PLEX       &lt;plex-name&gt;     <br> - SYSTEM  &lt;system-name&gt;          <br> - LPAR       &lt;lpar.name&gt;       <br> - SMFID      &lt;smd-id&gt;      |
| KMG270I | Enhanced wrap for DES not available. |
| KMG271I | Enhanced wrap for DES available:<br>- DEFAULT FOR INTERNAL TOKENS = &lt;ECB/CBC/EW3&gt;<br>- DEFAULT FOR EXTERNAL TOKENS = &lt;ECB/CBC7EW3&gt;<br>ECB is ORIGINAL, CBC is WRAP-ENH and EW3 is WRAPENH3|
| KMG272I | WRAPENH3 FOR DES AVAILABLE|
| KMG273I | WRAPENH3 FOR DES *NOT* AVAILABLE|
| KMG274I | WRAPENH3 OVERRIDE ENABLED|
| KMG275I | WRAPENH3 KEY-LEN NOT ALLOWED, ACP=003C<br>(Key length information for WRAPENH3 keys cannot be obtained using CSNBKYT KEY-LEN rule - either because facility is not available or not enabled as access control point) |
| KMG276I | WRAPENH3 KEY-LEN POSSIBLE<br>(Key length information for WRAPENH3 keys can be obtained by using the CSNBKYT KEY-LEN rule)|
| KMG277I | AES KEY-LEN NOT ALLOWED, ACP=003B<br>(Key length information for variable length AES keys cannot be obtained using CSNBKYT KEY-LEN rule - either because facility is not available or not enabled as access control point)|
| KMG278I | AES KEY-LEN POSSIBLE<br>(Key length information for variable length AES keys can be obtained by using the CSNBKYT KEY-LEN rule)|
| KMG300E | DSNALI failed to connet to Db2 system &lt;system&gt;.<br>RETURN CODE: xxxxxxxx<br>REASON CODE: xxxxxxxx |
| KMG301E | DSNALI failed to open plan &lt;plan&gt; on Db2 system &lt;system&gt;.<br>RETURN CODE: xxxxxxxx<br>REASON CODE: xxxxxxxx |
| KMG303I | Db2 ppppyyymm VERSION xxxx.  | Information about the Db2 program level and version in use. |
| KMG304I | Old adapter session had RESERVE flag.<br> Relieving ROLLBACK done, SQLCODE = xxxxxx |
| KMG310I | Db2 termination in progress TECB = xxxx. | When the Agent is stopped by command or stops because Db2 stops, then Db2 disconnect process will start. |
| KMG311I | DSNALI close abort successful. |
| KMG312E | DSNALI failed close<br>RETURN CODE: &lt;rc&gt;<br>REASON CODE: &lt;rs&gt; |
| KMG313I | DSNALI disconnect successful. |
| KMG314E | DSNALI failed disconnect<br>RETURN CODE: &lt;rc&gt;<br>REASON CODE: &lt;rs&gt; |
| KMG330I | Task termination without waiting modify interface termination. | The Agent decided not to wait for the MVS console interface to end. This can happen when system resources are busy. No further action is required. |
| KMG331I | Modify detach ended in error rc = &lt;rc&gt; |
| KMG332I | Possible abend like 33E can be expected and is harmless. | Message comes together with KMG331I. |
| KMG400I | Received command : &lt;cmd&gt;.  | This is a WTO message. A valid command was entered, and the Agent to process |
| KMG401W | Received invalid command : &lt;cmd&gt;. This is a WTO message. | The command received is invalid, and the Agent ignores the input. |
| KMG801I | Session &lt;sess#&gt; ended due to reserve timeout, user = &lt;user ID&gt;. | A result of &amp;RESERVE-WAIT-MIN in KMGPARM where the session was holding an EKMF reserve without activity |
| KMG802I | Db2 ROLLBACK done for reserve time out. |
| KMG803W | DBE ROLLBACK error = &lt;sqlcode&gt;. |
| KMG807I | Module/version list: | A list of Agent modules and program levels from the SKMGMOD0 library. |
| KMG808I | EKMF settings: | Lists output of KMGPARM options and configuration keys used.  |
| KMG820I | &amp;SELFTEST-DB2 not ON – test ignored<br>- or -<br>&amp;SELFTEST-CSF not ON – test ignored<br>-or -<br>&amp;SELFTEST-CLIENT not specified – test ignored |
| KMG821I | SELFTEST,DB2 cannot run when while an EKMF session has a reserve |
| KMG822I | SELFTEST,DB2 cannot run when &amp;DB2-USE(NO) |
| KMG827I | CSFSERV PROFILE PREFIXING: &lt;status&gt; |
| KMG828I | CSFKEYS PROFILE PREFIXING: &lt;status&gt;|
| KMG829I | Start testing access to CSFSERV resources |
| KMG830I | End testing access to CSFSERV resources |
| KMG831I | &lt;csfserv-resource&gt; OK |
| KMG832E | &lt;csfserv-resource&gt; No access | Permit the Agent user id to the resource |
| KMG839I | Start testing client access for &lt;user id&gt; |
| KMG840I | End testing client access for &lt;user id&gt; |
| KMG849I | Start testing access to the EKMF tables |
| KMG850I | Test Db2 success commit |
| KMG851E | Test Db2 failed &lt;action&gt; | Check the error codes listed. For ERROR-TYPE = 3 the RETURN-CODE would be an SQL code |
| KMG852I | All Db2 tests successful |
| KMG853I | Db2 qualifier from PLAN or &amp;DB2-QUALIFIER is OK<br>- or -<br>&lt;view name&gt; view is OK |
| KMG854E | Db2 qualifier from PLAN or &amp;DB2-QUALIFIER is in error<br>- or -<br>&lt;view name&gt; view error | Check the KMG851E message |
| KMG855E | All Db2 tests done – errors occurred |
| KMG856I | SYSTEM EBCDIC SBCS CCSID = &lt;ccsid&gt;<br><br>From Db2 GETVARIABLE('SYSIBM.SYSTEM_EBCDIC_CCSID') | This is most likely the EBCDIC codepage you want to specify in the EKMF Workstation device configuration |
| KMG857W | SYSTEM_EBCDIC_CCSID RETURNED NULL |
| KMG858I | ICSF CSFIQF ICSFST2 DATA: | Text messages showing master key status |
| KMG859I | KMG859I DOUBLE-O suggested as DES ECDH KEK<br>or<br>KMG859I TRIPLE-O suggested as DES ECDH KEK |
| KMG860I | Db2 SQLCODE =' &lt;sqlcode&gt; ' at loc = &lt;pgmname&gt;/&lt;loc&gt;<br>:SQLERRMC = &lt;SQLERRMC&gt; | This message can give additional information to debug non trivial SQL codes. |
| KMG861I | The received input data length was &lt;#chars&gt;, expected length = &lt;#chars&gt; |

