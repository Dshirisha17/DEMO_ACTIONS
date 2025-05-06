# DEMO_ACTIONS
Actions in Github
public void submitTranhistjob() throws Exception {
    // JCL without a JOB card — Galasa will insert it
    StringBuilder jcl = new StringBuilder();

    jcl.append("//RUN     EXEC PGM=IKJEFT01,DYNAMNBR=64\n");
    jcl.append("//STEPLIB DD DISP=SHR,DSN=COBOL.CHECK.DEV.LOAD\n");
    jcl.append("//        DD DISP=SHR,DSN=DSND10.SDSNLOAD\n");
    jcl.append("//        DD DISP=SHR,DSN=DSND10.DBDG.RUNLIB.LOAD\n");
    jcl.append("//        DD DISP=SHR,DSN=CEE.SCEERUN\n");
    jcl.append("//SYSUDUMP DD SYSOUT=*\n");
    jcl.append("//ABENDAID DD SYSOUT=*\n");
    jcl.append("//ABNLTERM DD SYSOUT=*\n");
    jcl.append("//SYSOUT   DD SYSOUT=*\n");
    jcl.append("//SYSTSPRT DD SYSOUT=*\n");
    jcl.append("//SYSOUT   DD SYSOUT=*\n");
    jcl.append("//SYSTSIN  DD *\n");
    jcl.append(" DSN SYSTEM(DBDG)\n");
    jcl.append(" RUN PROGRAM(TRANQURY) PLAN(TRNQURY1)\n");
    jcl.append(" END\n");
    jcl.append("//SYSIN DD *\n");
    jcl.append("000000000012345\n");
    jcl.append("/*\n");

    // Submit the JCL using the appropriate Galasa manager
    zosBatchManager.submitJcl(jcl.toString());
}


