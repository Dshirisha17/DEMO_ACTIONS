# DEMO_ACTIONS
Actions in Github
galasactl project create `
>>         --package dev.galasa.mainframe.jclsubmit `
>>         --features test `
>>         --force `
>>         --obr `
>>         --log - `
>>         --maven `
>
>zos.dse.tag.POPUP216.imageid=POPUP216
zos.dse.tag.POPUP216.clusterid=POPUP216

simbank.dse.instance.name=POPUP216
simbank.instance.POPUP216.zos.image=POPUP216

zos.image.POPUP216.ipv4.hostname=10.10.1.216
zos.image.POPUP216.telnet.port=3270
zos.image.POPUP216.telnet.tls=false
zos.image.POPUP216.credentials=POPUP216


zosmf.server.POPUP216.images=POPUP216
zosmf.server.POPUP216.hostname=10.10.1.216
zosmf.server.POPUP216.port=10443
zosmf.server.POPUP216.https=true
zosmf.server.POPUP216.username=IBMUSER
zosmf.server.POPUP216.password=SANDHATA

zosbatch.batchjob.POPUP216.use.sysaff=No
zosbatch.batchjob.POPUP216.restrict.to.image=POPUP216

zosbatch.batchjob.POPUP216.timeout=300
zosbatch.default.POPUP216.input.class=A
zosbatch.default.POPUP216.message.class=X
zosbatch.default.POPUP216.message.level=(2,1)
zosbatch.jobname.POPUP216.prefix=CR8PS

package dev.galasa.mainframe.jclsubmit.test;

import dev.galasa.zos.IZosImage;
import dev.galasa.zos.ZosImage;
import dev.galasa.zosbatch.IZosBatch;
import dev.galasa.zosbatch.IZosBatchJob;
import dev.galasa.zosbatch.ZosBatch;
import dev.galasa.Test;

@Test
public class TestTest {

    @ZosImage(imageTag = "POPUP216")
    public IZosImage image;

    @ZosBatch(imageTag = "POPUP216")
    public IZosBatch zosBatch;

    @Test
    public void submitCreatePSDatasetJob() throws Exception {
        // JCL without a JOB card — Galasa will insert it
        StringBuilder jcl = new StringBuilder();
        jcl.append("//STEP01 EXEC PGM=IEFBR14\n");
        jcl.append("//DD1    DD DSN=SHIRISH.GALASA.TESTPS,\n");
        jcl.append("//       DISP=(NEW,CATLG,DELETE),\n");
        jcl.append("//       SPACE=(TRK,(3,2),RLSE),\n");
        jcl.append("//       UNIT=SYSDA,VOLUME=SER=DEVHD4,\n");
        jcl.append("//       DCB=(DSORG=PS,RECFM=FB,LRECL=80,BLKSIZE=800)\n");

        // Submit the job
        IZosBatchJob job = zosBatch.submitJob(jcl.toString(), null);

        // Wait for completion
        int rc = job.waitForJob();

        if (rc != 0) {
            throw new Exception("Dataset creation failed with RC=" + rc);
        }
    }
}
galasactl runs submit local --log - `
>>   --obr mvn:dev.galasa.mainframe.jclsubmit/dev.galasa.mainframe.jclsubmit.obr/0.0.1-SNAPSHOT/obr `
>>   --class dev.galasa.mainframe.jclsubmit.test/dev.galasa.mainframe.jclsubmit.test.TestTest

