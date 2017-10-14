# Q0 Data Processing Sprint

## Proposed Data Workflow

Process | Who | Outputs
--------|-----|---------
Accept data from TA3 | sd2eadm | Deposit to Ingests
Develop and test ETL processes | <etl_team> | Archive job results to User Temp, User Data, Staging while working
Run production ETL processes | <etl_team> | Archive jobs produced by _public apps_ to Processed and ensure public read ACL set

## Data Locations

Nickname | System | Path | Purpose | Read | Write
---------| -------|---------|------|------|------
Ingests | data-sd2e-community | /ingest | Orignal data | All | sd2eadm
Processed |data-sd2e-community | /processed | Accepted data+products | All | sd2eadm
Reference | data-sd2e-community | /reference | Common reference data | All | sd2eadm,vaughn,jfonner,ngaffney
Sample | data-sd2e-community | /sample | Samples and examples | All | sd2eadm,...
Staging | data-sd2e-community | /processed_staging | Staging area for data+products | All | sd2eadm,<etl_team>*
User Data | data-sd2e-projects-users | /<uname> | Collaborative storage for users | <uname>* | <uname>*
User Temp | data-tacc-work-uname | * | User-specific high speed storage | <uname> | <uname>

## Coordination

[Google Docs Sheet][2] with the following columns:
* Path (relative to original upload conventions)
* Public apps to process
* Output naming conventions
* Participants
* Status

[Slack #data-etl channel][3]

## Sharing conventions

Following [Agave API][1] ACL model for portability and future-proofness. [Tutorials abound][5] for its application and usage in SD2. 

### Permissions

* `READ`
* `WRITE`
* `EXECUTE` (na)
* `READ_WRITE`
* `READ_EXECUTE` (na)
* `WRITE_EXECUTE` (na)
* `ALL` (READ_WRITE_EXECUTE)
* `NONE` - Removes access

### Usernames

* uname - yours or someone else's TACC username
* etl_team - any of the following people
    * vaughn
    * ngaffney
    * mweston
    * jeg
    * meslami
    * jfonner
    * wallen
* public - special user granting access to all authorized usernames
* world - special user granting world-readable access

## Processing Apps

| Name | App ID | Host | Purpose | Lead | Public | Shared
-------|--------|------|---------|------|--------|-------
FastQC | `fastqc-0.5.0` | maverick,wrangler | QC report for NGS data | Vaughn | No | na
FCS-TASBE | `fcs-tasbe-0.2.0u4` | jetstream | Summarize Flow data | Gentile/Vaughn | X | na
Kallisto | `kallisto-0.43.1u3` | maverick | Quantify RNAseq data | Vaughn | X | na
LCMS | `lcms-0.1.0u4` | maverick| Summarize LCMS data | Weston | X | na
MSF | `msf-0.1.0u3` | | maverick | Summarize MS data | Weston | X | na
Sailfish | `sailfish-0.10.1u3` | maverick| Quantify RNAseq data | Vaughn | X | na
SortmeRNA | `sortmerna-0.0.1` | maverick,wrangler | Filter rRNA from demux, trimmed RNAseq | Gaffney | No | vaughn
TrimSortmeRNA | `trimsortmerna-0.1.0` | maverick,wrangler | Trimmomatic + rRNA filtering | Gaffney | No | No

Request access and join development effort at [Reactors-ETL Github Repo][4]

[1]: https://apidocs.sd2e.org/
[2]: https://docs.google.com/spreadsheets/d/1qY_XAcrOWEQygmCiUu7_6k_2W0N_i_5F7O7bNMfFbEU/edit#gid=0
[3]: https://sd2e.slack.com/messages/C6W25F0LQ/
[4]: https://github.com/SD2E/reactors-etl/
[5]: https://merp.co/

