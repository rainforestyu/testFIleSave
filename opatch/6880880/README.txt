	
PATCH 28186730 - OPATCH 13.9.4.2.4 FOR FMW/WLS 12.2.1.3.0, 12.2.1.4.0 AND 14.1.1.0.0
		
Platform             : Generic
Product Patched      : Oracle Fusion Middleware 12c / Oracle WebLogic Server 12c AND 14.1.1
Product Version      : 12.2.1.3.0, 12.2.1.4.0 AND 14.1.1.0.0

	 
This is the README file for OPatch 13.9.4.2.4, the Oracle Interim One-off Patch Installer.

Notes
-----

Historically, OPatch was updated by unzipping and replacing ORACLE_HOME/OPatch directory.
For versions greater than or equal to 13.6, it now uses the OUI installation tooling. 
This ensures that installer both executes the file updates and logs the components and 
file changes to the OUI meta-data. A pure unzip install means the OUI tooling is 
not aware of these changes, which has on occasions led to upgrade related issues.

When extracted, this contains a 6880880 directory. This is because previous OPatch downloads 
are available as Patch 6880880. To avoid confusion with downloads not applicable to FMW/WLS, 
this new OPatch 13.9.4.2.4 placeholder was created as Patch 28186730. 


Pre-Installation Instructions 
----------------------------- 

1. Backup of <ORACLE_HOME> and Central Inventory must be taken as there is no mechanism to rollback to older opatch version.
 
2. Unzip this patch into your PATCH_HOME staging directory. 

3. This installer must be executed using a Java Development Kit (JDK). 
   - Set your PATH to include your <JDK_LOCATION>/bin

4. All the processes which are using files from ORACLE_HOME must be stopped before OPatch upgrade.


Installation
----------------------------------
 
1. Install the software with the following command:

    UNIX Only:
	java -jar <PATCH_HOME>/6880880/opatch_generic.jar -silent oracle_home=<ORACLE_HOME_LOCATION>
	
	Note: If you have /tmp is set with a noexec flag, you can override the tmp with the -D argument:
	java opatch_generic.jar -Djava.io.tmpdir=/opt/oracle -jar -silent oracle_home=<ORACLE_HOME_LOCATION>
	
	Windows Only:
	java -jar opatch_generic.jar -J-Doracle.installer.oh_admin_acl=true -silent oracle_home=<ORACLE_HOME_LOCATION>


where ORACLE_HOME_LOCATION is the absolute path where you have installed FMW/WLS products.

If using a custom Inventory location, install the software with the following command:
    
    java -jar <PATCH_HOME>/6880880/opatch_generic.jar -silent oracle_home=<ORACLE_HOME_LOCATION> -invPtrLoc <INVENTORY_LOCATION>

where INVENTORY_LOCATION is the absolute path to the oraInst.loc file.



2. To validate the installation:

    cd <ORACLE_HOME>/OPatch
    opatch version
    opatch lspatches
 
 
Post-installation Instructions
----------------------------------

When applying interim patches with OPatch 13.9.4, Microsoft Windows platform needs the '-oop' option:

<ORACLE_HOME>/OPatch/opatch apply <PATCH_HOME> -oop

where PATCH_HOME is a numbered directory where you extracted interim patch contents.

Follow interim patch readmes for other installation steps to apply patches.

Note on NGINST Dependency Patches
----------------------------------

No need to apply following NGINST patches as the fixes are available as part of 13.9.4.2.4 OPatch.

 31101362, 29137924, 29909359
 
Please refer "Details about NGINST Patches" section for further details.

 
Deinstallation
--------------

There is no mechanism to revert OPatch to an older version.

To revert OPatch, restore the backup for your ORACLE_HOME

 
Documentation and Help
-----------------------

To obtain command names or options from the command prompt, use:

    opatch -help
    opatch napply -help
 
To learn about patching with the OPatch utility with FMW/WLS 12c:

Doc ID 1587524.1 Using OUI NextGen OPatch 13 for Oracle Fusion Middleware 12c (12.1.2+)

 

New Features and Bugs Fixed List
---------------------------------
13.9.4.2.4
----------
 30943081 : PERFORMANCE ISSUE IN FMW12C OPATCH
 31610167 : OPATCH TO SUPPORT CBCC (CONTENT BASED CONFLICT CHECKING) 
 30687963 : INFO - WEBLOGIC DEPLOYMENT FAILED WITH INSUFFICIENT DISK SPACE
 30922561 : COPY/PASTE BINARY FOR OID 12.2.1.4 ARE FAILING
 31085467 : Agent Patch Rollback Fails using 13.9.4.2.2 OPatch
 31512132 : WLTHINT3CLIENT.JAR HK2 META DATA IS NOT GETTING PROPERLY REGENERATED DURING PSU PATCH INSTALL
 28218773 : WLST SLOW IN SOLARIS
 29206542 : ACCOMMODATE A NEXTGEN CENTRAL INVENTORY WITH MISSING LOCKS DIRECTORY
 29253949 : Fix for Bug 29253949
 29292673 : POM GENERATION ISSUE, ANT 1.9 DROPPED FROM POM WHEN ANT 1.10 FEATURESET ADDED TO SHIPHOME
 29334003 : WEBLOGIC PSU FAILING WITH JAVA.NIO.FILE.ACCESSDENIEDEXCEPTION:/WLSERVER
 29396325 : UPGRADE XERCES FROM 2.11 TO 2.12
 29410238 : DUPLICATE MAVEN ARTIFACTS GENERATED WITH DIFFERENT GROUPID DURING PATCH APPLICATION
 29655515 : DISABLE POM-GEN AT THE DISTRIBUTION LEVEL
 29902141 : Fix for Bug 29902141
 29909359 : BUILD FAILURE OBSERVED IN A WLS WEBSERVICES SUITE WITH OPATCH 13.9.4.2.0
 30240291 : EM INSTALLER FAILS TO LOAD OUI WHILE PROVIDING ALTERNATE TMP SPACE
 30317205 : PORT ER/BUG 29724751
 30317648 : PORT BUG 30180115 -- UPDATE JACKSON IN NGINST 13.9.4 PL2
 30368770 : AFTER EXECUTING THE PASTEBINARY WE SEE ERRORS IN <OH>/INSTALL/MAKE.LOG
 30600358 : ESSBASE INSTALLER RAN INTO AN NGINST BUG IN RESOLVING "DB_CLIENT"
 30614758 : OPATCH UPGRADE FAILED TO 13.9.4.2.1 FROM 13.9.4.2.0
 30639894 : COPYBINARY.SH IS NOT COPYING ALL FILES IN THE ORACLE HOME
 30650032 : GETAVAILABLEPATCHE API IS NOT WORKING
 30670676 : Fix for Bug 30670676
 30753555 : 13.4 EM INSTALL ON ONEOFF APPLICATION IS FAILING SOLARIS SPARC ZONE 11.3 FAILS
 
13.9.4.2.2
-----------
 30163394 : OPATCH TAKES TOO MUCH TIME TO COMPLETE
 30489794 : OPATCH TAKES 20+ MINUTES ON SOLARIS SPARC 64 BIT SYSTEMS(SUPER CLUSTER) FOR FMW PATCHES
 30687067 : 13.4 STACK 12.2.1.3.0 AGENT PATCH PLAN ANALYSIS FAILS
 28788794 : NEED NO BACKUP FILES OPTION TO REDUCE DOCKER IMAGE SIZE INCREASE
 24953000 : [EM13.2PG]AGENT PUSH TO RAC ENV,ORACLE USER LOCK INVENTORY DIRECTORY
 30614758 : OPATCH UPGRADE FAILED TO 13.9.4.2.1 FROM 13.9.4.2.0
 30639894 : COPYBINARY.SH IS NOT COPYING ALL FILES IN THE ORACLE HOME

13.9.4.2.1
----------
 30081813 : PERL PATCHING FAILS IN FMW 12.2.1.3.0
 29909359 : BUILD FAILURE OBSERVED IN A WLS WEBSERVICES SUITE WITH OPATCH 13.9.4.2.0
 30251029 : ERROR IN THE OUTPUT WHEN EXECUTING THE COMPAREINVENTORY SCRIPT.
 29450902 : OPATCH 13.9.4 INSTALLER CHECKS PERMISSION OF PARENT FOLDER OF ORACLE_HOME
 29334003 : WEBLOGIC PSU FAILING WITH JAVA.NIO.FILE.ACCESSDENIEDEXCEPTION:/WLSERVER

13.9.4.2.0
----------
 Replacement in Use Feature (-oop), OPatch wil be able to patch files which are in use (being used by other application)
 29137924 : Generated POM file dependency artifacts are incorrect (BUILD FAILURE OBSERVED IN WEBSERVICES MAVEN PLUGIN SUITE WS-MAVENPLUGIN-RISK1)
 28632744 : OPATCH NOT PERFORMING STRING SUBS ON FILE ADDED TO COMPDEF IN OPATCH
 28674381 : VERIFY AND FIX REFCOUNTS BEFORE DISTRIBUTION INSTALLATION
 28710121 : FIX DEINSTALL OF MULTIPLE DISTRIBUTIONS IN THE SAME OH
 28732248 : IN CLONING OF BUILD_HOME, ANT-SOA-COMMON.XML NOT INSTANTIATED
 28758292 : LSINV FAILED AFTER PATCH APPLIED WITH OPATCH/CAS ON NG HOME
 28844525 : INFRA DISTRIBUTION-LEVEL BUNDLE PATCH HAS ONLY XML FILES IN THE PAYLOAD


Details about NGINST Patches
----------------------------
Patch 31101362: NGINST SPU FOR 13.9.4.2.2 FOR JACKSON-DATABIND UPDATE TO 2.10.2

	1. The fix for this bug is already present in the current installer, no need to apply patch 31101362 as the fix is already available. 
	1a. Further to point #1, if you have already applied this patch it will show up in the inventory , you cannot roll it back after the upgrade, its harmless and we will fix the functionality later to rollback such intern patches.
	1b. If you have not yet applied 31101362 and not upgraded OPatch 13.9.4.2.4, then you just need to upgrade the new OPatch which has the fix, do not try to apply this patch 31101362 after the OPatch upgrade as that would result in an error.
	
Patch 29137924 : Generated POM file dependency artifacts are incorrect (BUILD FAILURE OBSERVED IN WEBSERVICES MAVEN PLUGIN SUITE WS-MAVENPLUGIN-RISK1)

	1. The fix for this bug is already present in the current installer, no need to apply patch 29137924 as the fix is already available. 
	1a. Further to point #1, if you have already applied this patch it will show up in the inventory , you cannot roll it back after the upgrade, its harmless and we will fix the functionality later to rollback such intern patches.
	1b. If you have not yet applied 29137924 and not upgraded OPatch 13.9.4.2.4, then you just need to upgrade the new OPatch which has the fix, do not try to apply this patch 29137924 after the OPatch upgrade as that would result in an error.

Patch 29909359: BUILD FAILURE OBSERVED IN A WLS WEBSERVICES SUITE WITH OPATCH 13.9.4.2.0

	1. The fix for this bug is already present in the current installer, no need to apply patch 29909359 as the fix is already available. 
	1a. Further to point #1, if you have already applied this patch it will show up in the inventory , you cannot roll it back after the upgrade, its harmless and we will fix the functionality later to rollback such intern patches.
	1b. If you have not yet applied 29909359 and not upgraded OPatch 13.9.4.2.4, then you just need to upgrade the new OPatch which has the fix, do not try to apply this patch 29909359 after the OPatch upgrade as that would result in an error.
