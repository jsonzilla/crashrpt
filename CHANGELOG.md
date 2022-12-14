### Changelog

### Ver. 1.4.3

- New: Crash log files are now saved under Logs subdirectory of error report directory.
       A crash log file is named like CrashRpt-Log-<date>-<time>-{<crashguid>}.txt.
       Recent log files are stored even if corresponding crash reports were delivered
       (to give user an ability to review recent crash information). When more than 10 logs
       are accumulated, the oldest ones are removed.

- New: Added CR_INSTALL_INFO::nRestartTimeout structure field. Using this parameter,
       you can override the default app restart timeout (60 seconds).

- New: added Slovak language file (contributed by Zoltan Tirinda)
- New: added Japaneze language file (contributed by devil.tamachan)
- New: added Czech language file (contributed by Petr Pytelka)
- New: Added Polish lang file (issue 241)

- Fixed: Crashsender SMTP sendMsg - Errorhandling (issue 200)
- Fixed: pfnCrashCallback2 is missing in tagCR_INSTALL_INFOW (issue 211)
- Fixed: Version 1402 does not include files attached with "crAddFile2" in case of
       a long path name (issue 209)
- Fixed: Few issues with static code analysis (issue 220)
- Fixed: Wrong screen video capture video with multi screen (issue 215)
- Fixed: crAddScreenshot2() nJpegQuality is only used for the first error report
       then it is always set to 0 (issue 217)
- Fixed: Added file changes (renamed, moved, removed, etc.) within a
       client program's running session (issue 219)
- Fixed: Adding custom properties with same name results in CrashSender.exe assertion
       failure (issue 216).
- Fixed: 'Attach More Files' : Adding large amount of files (over >= 10)
       unsuccessfully (issue 218)
- Fixed: Also add your x64 version of dbghelp.dll to the distributed file (issue 199)

### Ver. 1.4.2

- New: Added an ability to add multiple files to crash reports with crAddFile2()
       using file search pattern (e.g. "*.log"). This implements feature request
       described in issue 190.

- New: Added new flag CR_INST_AUTO_THREAD_HANDLERS allowing to
       install/uninstall exception handlers automatically in DllMain()
       on DLL_THREAD_ATTACH/DETACH (issue 185).

- New: adjusting dump privileges to avoid error 'Only part of a ReadProcessMemory
       or WriteProcessMemory request was completed.'

- Fixed: Screenshot file still sent even if deleted (issue 186).
- Fixed: Video division by zero (issue 189)
- Fixed: Video missing from report (issue 187)
- Fixed: No crash data is sent to URL when we have a redirect (Issue 191)
- Fixed: CCrashHandler.m_hWndVideoParent not initialized to a
         default value (issue 195)


### Ver. 1.4.1

- New: Added an ability to preview OGG video files in Error Report Details dialog.
       To preview a file, select it in the list of files.

- New: Added an bility for end user to delete screenshots, registry keys and video file
       from crash report through context menu of Error Report Details dialog
       (added CR_AS_ALLOW_DELETE flag for crAddScreenshot2() function,
        CR_AR_ALLOW_DELETE flag for crAddRegKey() function and CR_AV_ALLOW_DELETE
        flag for crAddVideo() function). (issue 183)

- New: Added back the crExceptionFilter() function removed previously as deprecated.
       It seems that some users require that function. (issue 175).

- New: Extended unit tests (added ExceptionHandlerTests) (issue 114)

- Fixed: Exception handling problems (issue 180)
- Fixed: Update italian language file (issue 174)
- Fixed again: HTTPS certificate problem (issue 151)
- Fixed: Custom property cleared by adding other property (issue 176)
- Fixed: Running crprober on windows 7 results in no stack trace output (issue 182)


### Ver. 1.4.0

- New: CrashRpt is now able to capture end user's desktop and record what happened
       just before crash to an .ogg video file and include the file to crash report.
       The recorded information may help the software vendor to better understand
       what actions the end user performed before client application crashed and
       reproduce the error (issue 122).

- New: Added new crAddVideo() function to record the desktop state to a video file
       and add the file to crash report.

- New: Added code of Theora video codec and OGG container (libtheora and libogg).

- New: New-style crash callback replacing the obsolete LPGETLOGFILE() callback.
       Added PFNCRASHCALLBACK() callback function prototype, CR_CRASH_CALLBACK_INFO
       structure and crSetCrashCallback() function.

- New: Added an ability to continue program execution after crash. This can be performed
       through crash callback (see CR_CRASH_CALLBACK_INFO::bContinueExecution structure
       member). This partially implements feature request in issue 125.

- New: Removed deprecated constant CR_INST_ALL_EXCEPTION_HANDLERS, use CR_INST_ALL_POSSIBLE_HANDLERS
       constant instead.

- New: Removed legacy method of error report delivery as Base-64-encoded data.
       Now binary-encoded HTTP uploads are always used instead. This makes the
       constant CR_INST_HTTP_BINARY_ENCODING useless.

- Fixed: Memory Leak (or rather memory not deallocated before program exit) (issue 169)
- Fixed: Can not restart application. Use CR_INST_APP_RESTART flag (issue 165)


### Ver. 1.3.1

- New: Removed support of obsolete Visual Studio .NET 2003.

- New: Removed deprecated functions crAddFileA(), crAddFileW(),
       crInstallToCurrentThread(), crExceptionFilter() and deprecated
       constant CR_WIN32_STRUCTURED_EXCEPTION.

- New: Improved robustness to stack overflow (issue 121). Now stack overflow is handled
       in separate thread makeing CrashRpt more robust to problem of not enogh stack memory.

- New: Added constant CR_STACK_OVERFLOW that can be passed to crEmulateCrash() function
       to cause stack overflow.

- New: Added an ability to attach more files to error report or delete selected files
       from error report through context menu of Error Report Details dialog (issue 132).
       Introduced new flag CR_INST_ALLOW_ATTACH_MORE_FILES for crInstall() function.

- New: Added new CR_AF_ALLOW_DELETE flag for crAddFile2() function. If this flag is specified,
       the user will be able to delete the file from error report using context menu of
       Error Report Details dialog. (issue 132)

- New: Added support of SMTP authentication (AUTH LOGIN) (Issue 143).

- New: Added an ability to store the user's E-mail address and re-use later. When user
       enters his E-mail into "Your E-mail" field of Error Report dialog, the address
       is  saved and stored in ~CrashRpt.ini file. When a crash occurs
       later, the address is filled in automatically. (issue 155)

- New: Added CR_INST_SEND_MANDATORY flag. This flag removes the "Close" and "Other actions"
       buttons from Error Report dialog, thus making the sending procedure mandatory for user
       (issue 126).

- New: Added CR_INST_SHOW_ADDITIONAL_INFO_FIELDS flag. This flag makes "Your E-mail" and
       "Describe what you were doing when the problem occurred" fields of Error Report
       dialog always visible. By default (when this parameter not specified),
       those fields are hidden and user needs to click the "Provide additional info
       (recommended)" link to show them (issue 129).

- New: Introduced command line parameter /terminate for CrashSender.exe.
       This resolves a problem with installers that will want to update the exe file;
       there was no way to tell the sender exe program to exit now (issue 142).
       Launching "CrashSender.exe /terminate" would look for all open CrashSender.exe processes
       and terminate them immediately (without sending reports or waiting for completion).
       Terminating the process is acomplished with TerminateProcess(hProcess) function.

- New: Reorganized demos (moved to demos folder and renamed CrashRptTest=>WTLDemo, crashcon=>ConsoleDemo).

- New: Added new demo application - MFCDemo. This is to demonstrate usage of CrashRpt
       with MFC-based apps.

- New: Refactored code of CrashSender project making it more conforming to
       the Model-View-Controller methodology.

- Fixed: Impossible to send Crash reports in Windows 7 64bits (issue 104).
- Fixed: Crash report is not discarded when 'Close the program' is selected (issue 94).
- Fixed: Application is restarted twice after crash (issue 115).
- Fixed: CRP_COL_PROBLEM_DESCRIPTION not working (issue 118).
- Fixed: When copying a log file into the crash archive, access it with FILE_SHARE_WRITE (issue 124)
- Fixed: Support multiple e-mail recipients (issue 123).
- Fixed: Support multiple crash reports per application instance (issue 127)
- Fixed: CrashSender.exe crashes when attempting to write long strings into NOTIFYICONDATA (issue 137)
- Fixed: a small typo in the german language file (issue 159)
- Fixed: A single .pch file is used by Release and Debug configs causing compiler errors (issue 147)
- Fixed: SigIntHandler installed by CR_INST_SIGILL_HANDLER (issue 154)
- Fixed: ASSERTION failure when CrThreadAutoInstallHelper fails to install handler (issue 148).
- Fixed: Deprecated CMC functions cause Visual studio 2012 rc compile error (issue 156)
- Fixed: Need to add "SMTP:" to the 'emailTo' address for (S)MAPI (issue 140).
- Fixed: HTTPS certificate problem (issue 151)
- Fixed: Resource leak in CrashRpt (issue 160)
- Fixed: HttpEndRequest() fails. GetLastError() = ERROR_INTERNET_TIMEOUT (12002) (issue 138)
- Fixed: Memory allocation in CCrashHandler::GetExceptionPointers can fail (issue 157)
- Fixed: Timestamp of saved files (issue 135)
- Fixed: CErrorReportSender::DumpRegKey is omitting some subkeys and some values (issue 162)
- Fixed: CErrorReportSender::DumpRegKey issue with REG_BINARY (issue 130).
- Fixed: Order of custom properties (issue 131).


### Ver. 1.3.0

- Added support of CMake - cross-plaform make system. Although CrashRpt doesn't support operating systems
  other than Windows, CMake makes it easier to maintain build configurations for different versions of Visual Studio.
  Project files for VC++ .NET 2003, 2005, 2008, 2010 and VC++ Express can be generated.

- Added instructions to the documentation on how to generate Visual Studio project files with CMake.

- Removed project files for Visual Studio 2003 (CrashRpt_v2003.sln) and Visual Studio 2005 (CrashRpt_v2005.sln).
  To compile in VS2010, use Visual Studio 2010 project files (or use CMake to generate Visual Studio project
  files for your favorite version of Visual Studio).

- Binary files now have version suffices (CrashRpt1300.dll, CrashRptProbe1300.dll and CrashSender1300.exe). This is
  to resolve problems of loading incorrect version of the DLL.

- Removed obsolete API InstallW, InstallA, Uninstall, AddFileW, AddFileA, GenerateErrorReport.

- Added an ability to select/deselect/delete all error reports and delete selected reports in ResendDlg (issue 112).

- Updated Italian lang file (issue 92).
- Updated German lang file (issue 98).
- Updated French lang file (issue 107).

- Fixed: CrashSender fails to initialize if two files both have empty destination properties (issue 88)
- Fixed: DestroyView fails in SharedMem implementation (issue 93)
- Fixed: CHttpRequestSender::InternalSend() sends bad request header (issue 95)
- Fixed: Potential buffer overflow in CHttpRequestSender::InternalSend() (issue 96)
- Fixed: Formatting / coding request (issue 97)
- Fixed: Typo in string conversion class (issue 99)
- Fixed: Compilation fails if build directory contains spaces (issue 100)
- Fixed:The space confuses some mail servers, the RFC for QUIT defines that there should be no space. (issue 105)
- Fixed: RFC correct base64 for SMTP send (issue 106)
- Fixed: Wrong handling of dwFlags when setting handlers (issue 109)
- Fixed: SMTP fails if Date header missing (issue 110)

### Ver. 1.2.10

- Added new language files: German, Spanish, French, Hindi, Italian, Korean, Portuguese and Chinese Simplified.
  Some of these files were produced by professional translators (Korean, Chinese Simplified), but others
  are generated with help of an automated translation tool, so do not hesitate to report mistakes.

- Refactored unit tests, so now they support fixtures and execute faster then before.

- Added new test suites LangFileTests and CrproberTests.

- Fixed: Typo in HttpRequestSender.cpp (issue 79)

- Fixed: Typos in test project (issue 82)

- Fixed: Replace relative paths with OutDir and IntDir (issue 80)

- Fixed: MD5 files are not removed (issue 83)

- Fixed: CrashSender cannot properly send old reports (with smtp) (issue 84)

- Fixed: CrashSender manifest file prevents CrashSender from launching in x64 (issue 87)

### Ver. 1.2.9

- Compiler/linker output for x64 platform is now directed to bin\x64, while output dir for Win32 platform
  is the same (bin) (issue 77).

- Improved documentation (extended "Using CrashRpt API" and "An Example of Using API", "Writing Robust Code" sections)

- Annotated code with SAL macros and fixed some PREfast warnings (this should fix some potential stability and
  security issues).

- Fixed: Clarification for CR_INST_DONT_SEND_REPORT & CR_AF_TAKE_ORIGINAL_FILE

- Fixed: SVN/package file encoding strangeness (issue 76)

- Fixed: If I pass the short name for the path to crash report, it failed to create the directory (issue 78)


### Ver. 1.2.8

- Added JPEG library code from Independent Jpeg Group.

- Improved desktop screenshot capture: added an ability to save screenshots as JPEG files, an
  ability to define JPEG image quaility, an ability to save grayscale screenshots.

- New function crAddScreenshot2() allows to define JPEG quality.

- Implemented Jpeg image preview in Error Report Details dialog.

- New section ScreenshotInfo in crash description XML file

- Modified compiler options in all projects to favor small size (Release configuration). This should
  reduce the size of the binaries.

- Completely rewritten the code responsible for communication between CrashRpt.dll and CrashSender.exe
  (now using shared memory instead of temporary XML files)

- Added an ability to add a custom title icon for CrashRpt dialogs through CR_INSTALL_INFO::pszCustomSenderIcon.

- New sections of documentation: Running automated tests and Making Your Code Robust.

- Refactored Tests project (removed unneeded functionality). Additional test cases.
  New test suite DeliveryTests. Tests now work even for Release LIB build configuration.

- Improved Doxyfile, removed search index and now the documentation should take less disk space.

- Added new table CRP_TBL_MDMP_LOAD_LOG

- New column CRP_COL_MODULE_LOADED_IMAGE_NAME

- MD5 file is now generated and stored in error report folder when using CR_INST_STORE_ZIP_ARCHIVES flag

- New member hSenderProcess in CR_EXCEPTION_INFO struct

- Fixed a mistake in basic_stats.py (now using multimap instead of map)

- Reorganized tinyxml files (now they are compiled in a separate project)

- Extended lang files (new strings DescCrashDump, DescXML, DescScreenshot, DescRegKey)

- Added HTTPS support for error report upload

- The function crExceptionFilter() is declared deprecated.

- fix: CR_INST_STORE_ZIP_ARCHIVES (issue 59)
- fix: crAddScreenshot( CR_AS_MAIN_WINDOW); (issue 61)
- fix: Cannot be loaded under Win2000 due to import of the GetGeoInfo function from kernel32.dll (issue 65)
- fix: std::string CCrashHandler::XmlEncodeStr(CString sText) error (issue 67)
- fix: CR_INST_STORE_ZIP_ARCHIVES and CR_AF_TAKE_ORIGINAL_FILE (issue 69)
- fix: atlassert in crashhandler.cpp (issue 70)
- fix: Registry keys with ampersand (&) are not dumped (issue 71)


### Ver. 1.2.7

- Added Tests project that implements automated tests for CrashRpt and
  CrashRptProbe functionality.

- Reorganized directory structure to better reflect architecture.

- Updated tinyxml, minizip and zlib files to the latest available versions.

- Refactored scripts/postprocess.bat. It now better groups similar error reports.

- New tag GeoLocation - user's geographic location like 'en-us' is now recorded inside of
  crash description XML.

- New tag OSIs64Bit - detects if user's OS is 64-bit and records this inside of
  crash description XML.

- Improved the way crprober.exe cleans up its temporary files.

- New columns CRP_COL_OS_IS_64BIT and CRP_COL_GEO_LOCATION for CRP_TBL_XMLDESC_MISC table.

- New column CRP_COL_EXCEPTION_THREAD_STACK_MD5 for CRP_TBL_MDMP_MISC table.

- Fixed issue with Chineese symbols in app name (issue 54).

- Improved CFilePreviewCtrl to support UTF-8 and UTF-16 encoding (issue 56). Also improved
  WM_MOUSEWHEEL message handling (scrolling preview by mouse wheel).

- Using critical section to avoid access to CCrashHandler from several crashed threads (issue 52).

- Fixed: Leaving pszRestartCmdLine NULL, gives new application instance blank first argument (issue 50).

- Fixed incorrect argument order in crAddRegKeyA (issue 49).

- Added new flag CR_INST_STORE_ZIP_ARCHIVES that allows to store ZIP archives along with uncompressed
  error report files (issue 53).

- Fixed: Version info caused crash (issue 48).

- Improved documentation (section Architecture Overview).

- Improved documentation (section Using Crash Minidump) (issue 45).

- Fixed DNS access problem for SMTP proxy (issue 51).

### Ver. 1.2.6

- Added project files for Visual Studio 2010 (issue 35).

- Using .def files to undecorate API function names.

- Extended crEmulateCrash(), new constant CR_THROW -- tests how a thrown C++
  exception is intercepted (issue 35).

- Fixed: exit(1) in different thread may cause crashes (issue 43). Now using
  TerminateProcess() instead of exit() or ExitProcess().

- Fixed: Error report is sent twice if crashes in a DLL (issue 44). Using crash
  counter variable to avoid multiple crash report generation.

### Ver. 1.2.5

- Introduced an ability to send error reports queued for delivery (issue 33).
  New flag CR_INST_SEND_QUEUED_REPORTS.

- Fixed: zipped file timestamps are incorrect (issue 40).

- Fixed: Release buffer from DnsQuery (issue 42).

- Fixed: exit(1) in different thread may cause crashes (issue 43).

- Fixed: A bug in CScreenCapture multiple monitors

- Fixed: Issue with g_CrashInfo.m_uPriorities. Introduced CR_NEGATIVE_PRIORITY constant.

- Refactored php example of how to receive error reports by HTTP.

- Extended documentation.

### Ver. 1.2.4

- Introduced an ability to restart an application automatically on crash. The application is
  restarted only if at least 60 seconds have elapsed since its start. This is done to avoid cyclic
  restarts of an unstable application which crashes on start up. This is the enhancement requested
  in issue 11.

- Introduced an ability to preview graphics files (BMP, PNG) in Details dialog. This is useful if a user
  would like to preview the desktop screenshot image attached to the error report.

- An ability to not include minidump file into error report. This implements the enhancement requested in
  issue 33.

- An ability to specify custom email text by using CR_INSTALL_INFO::pszEmailText member.

- An ability to specify custom directory and file name for the language file. This will be useful for applications
  that need to modify UI language on the fly. This is requested in issue 34.

- An ability to disable particular error report sending transport by specifying a negative priority in
  CR_INSTALL_INFO::uPriorities array.

- An ability to specify SMTP proxy for built-in SMTP client. This may be useful for server-side software that
  would need to configure SMTP transport without querying DNS MX (mail exchange) record.

### Ver. 1.2.3

- Improved file preview in DetailDlg. Now a file can be previewed in HEX or in text mode.

- Ability to customize the port for SMTP connection.

- Fixed: CrashSender Crash (issue 24)

- Fixed: dbghelp.dll cannot be found (issue 26)

- Fixed: Certain fields cannot be omitted (issue 27).

- Fixed: Release LIB configuration is obsolete (issue 28).
  There may be some people using Release LIB configuration, so the configuration was made up-to-date.


### Ver. 1.2.2

- WTL files are now included into CrashRpt distribution.

- Completely removed dependency on zip_utils (it is better to use minizip).

- Removed vs.2008 project files. If you need to compile in VS 2008 and higher, use VS project convertor.

- Modifyed communication between CrashRpt.dll and CrashSender.exe. Now XML file is used for this purpose instead of named pipe.

- Refactored code. After crash, all complex actions are done outside of the crashed process (inside of CrashSender.exe).
  This includes taking desktop screenshot, minidump generation, file copying, file compression and sending.

- Introduced silent mode (CrashRpt sends report silently without showing GUI).
  This is useful for services and server processes.

- Improved documentation (restyling).

- Introduced multi-part HTTP uploads. This will help to send large error reports more effectively.

- Fixed: Doesn't work in Windows 2000 (issue 17)
- Fixed: CrashSender doesn't work on Windows 2000 (issue 21)

- Fixed: mistyping? (issue 18)
- Fixed: inconsistency in xml Crash Log (issue 20)
- Fixed some problems with UTF-8 encoded strings written by tinixml.

- Fixed: crprober.exe does not work well (issue 19)

- New: Introcuded an ability to specify the folder where crash reports are created (issue 22)

- New: Introduced an ability to export error report through "Export..." button on Error Report Details dialog.

### Ver. 1.2.1

- Refactored crash report generation and sending functionality. Now report files are stored
  in unzipped state, compression is performed during sending procedure. This will be required for
  huge reports (that will be fully supported in the future).

- Added support of x64 platform (issue 7).

- Added an ability to make screenshots of the screen or the main app window on crash
  through crAddScreenshot() function (issue 8).

- More information is collected on crash (memory usage, open handles count and GUI resources)

- Ability to add custom text properties to the crash descriptor through crAddProperty() function    (issue 9).

- New function crAddFile2() improving the application-defined files addition.

- Ability to control which dbghelp.dll to use (issue 10).

- Ability to define the type of minidump (from normal size to huge size) (issue 10).
  Contributed by crcode.s.

- Fixed incorrectly displayed file size in DetailsDlg (issue 14).

- Fixed untranslatable Close button of DetailsDlg (issue 15).

- Fixed: Access to CCrashHandler::m_ThreadExceptionHandlers should be synchronized (issue 16).

### Ver. 1.2.0

- Reorgranized the include files; moved from 'CrashRpt\include' to 'include'.

- Support of error report batch processing (crprober.exe tool).

- New application programming interface for error report processing (CrashRptProbe.dll).

- Introduced functions crpOpenErrorReport(), crpCloseErrorReport(),
  crpGetProperty(), crpGetLastErrorMsg().

- Fixed problem with missing gzio.c (issue 6).

- Extended documentation : new section 'Automating Error Report Processing'.

### Ver. 1.1.3

- Support of globalization and RTL languages.

- Reorganized and improved documentation; New pages Architecture Overview and
  Internationalization Support.

- Added <?xml version="1.0" encoding="utf-8" ?> element in the
  beginning of crash descriptor XML.

### Ver. 1.1.2

- crInstall: Ability to select what exception handlers to install

- Extended CR_INSTALL_INFO with new members: pszPrivacyPolicyURL and dwFlags.

- New API function crInstallToCurrentThead2().

- Improved documentation; Fixed some mistakes; Added info on compiling CrashRpt in VC++ Express

- Using standard Windows convention __stdcall instead of __cdecl in API function declarations

- Using undecorated API function names (extern "C")

- Using static zlib linkage instead of zlib DLL

- Replaced obsolete ATL 3.0 string conversion macros with self-written class strconv_t.

- Fixed some compilation warnings in VC++ Express

- Fixed wrong "unh" message box in unhandled exception handler

- Fixed bug in CUtility::GetOSFriendlyName() -- Operating system build
  number and service pack are never retrieved

- Fixed error with writing 'ExceptionCode' to XML (always zero)

- Writing exception code to XML in hex format

- Refactored code of crEmulateCrash()


### Ver. 1.1.1

- Support of Visual Studio Express edition (EVS 2005 and EVS 2008)

- Improved documentation; New page About Exceptions and Exception Handling

- New wrapper classes CrAutoInstallHelper and CrThreadAutoInstallHelper

- MD5 hash for error report is calculated and attached to email
  when error report is sent over email

- Error report is removed when sent successfuly

- Refactored error report sending code

- Extended E-mail message text generation for error reports being sent over email

- 'Copy selected lines' and 'copy the whole log' from context menu of error report
  sending log

- Fixed many VS-version-specific bugs

### Ver. 1.1


Major Features:

- Removed support of Visual Studio 6.0 and added support of VS.NET 2003,
  VS 2005 and VS 2008

- New API functions (crInstall(); crUninstall(); crInstallToCurrentThread();
  crUninstallFromCurrentThread(); crGenerateErrorReport(); crExceptionFilter();
  crEmulateCrash(); crGetLastErrorMsg())

- Character set specific functions have A and w suffixes. Introduced macros for
  defining character set indepandent function names mapping

- Support of various C++ exception handlers (Visual Studio-specific)

- Crash report generation and crash sending functionality are separeted into
  different modules (CrashRpt.dll and CrashSender.exe)

- New ways of sending error reports: using HTTP connection, using SMTP embed client or
  (as in 1.0) using Simple MAPI.

- Each error report is now assigned a unique CrashGUID

- Doxygen-based documentation system

- Revamped GUI of Send Error Report dialog

- New Error Report Sending Progress dialog

- Improved crash descriptor XML format


Minor features:

- Using TinyXml framework instead of MSXML

- Using the latest version (at the moment) of dbghelp

- Using the latest version (at the moment) of zlib


#### Ver. 1.0
    * 03/17/2003
          o Replaced MFC with WTL.
          o Changed crashrpt interface.
          o Major refactoring.
          o Updated article.
          o Details dialog preview window now uses system defined window color instead of white.
          o Directory structure not saved in ZIP.
          o Support for use by multiple apps.
          o Buffer overrun error when previewing files > 32k.
          o Main dialog now displays app icon.
    * 01/12/2003
          o Initial release.

