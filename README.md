#### Getting Started
Download the module to the desired local directory and then import similar to:

```
Import-Module c:\mods\VMToolsOnline
```

#### Included Function
This module currently only includes one function, Get-VMToolsOnline.
The following is the related help output.

```
NAME
    Get-VMToolsOnline

SYNOPSIS
    Uses Powershell webcmdlets to connect to vmware.com and get a list of all
    VMware Tools versions along with supporting information.


SYNTAX
    Get-VMToolsOnline [-Uri <String>] [-PassThru] [<CommonParameters>]

    Get-VMToolsOnline [-ShowHeader] [<CommonParameters>]

    Get-VMToolsOnline [-Raw] [<CommonParameters>]


DESCRIPTION
    Uses Powershell webcmdlets to connect to vmware.com and get a list of all
    VMware Tools versions along with supporting information.  Also includes
    a derived property for RSS showing if a given Tools version is affected.

    All version information is obtained live from the internet, while the RSS
    bug is checked against a specific list of affected versions included in the script.

    The RSS issue was introduced in VMware Tools 9536 (9.10.0) and resolved in VMware Tools
    10282 (10.1.10). We treat versions greater than 10282 as being resolved and therefore
    return false for the RssImpactedTools property.


PARAMETERS
    -Uri <String>
        String. The URI of the offical VMware Tools release page. No need to change this.

        Required?                    false
        Position?                    named
        Default value                https://packages.vmware.com/tools/versions
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -ShowHeader [<SwitchParameter>]
        Switch. Optionally, show header comments from the official VMware patch release page.
        The comments are valid only for the first four columns, which are provided by VMware.
        Additional columns added by the community (i.e. 'RSSAffectedTools') will not be documented
        in the header.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Raw [<SwitchParameter>]
        Switch. Optionally, return the raw format of the web uri returned.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -PassThru [<SwitchParameter>]
        Switch. Optionally, return object info with no formatting.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


NOTES


        Script:     Get-VMToolsOnline.ps1
        Author:     Mike Nisk

    -------------------------- EXAMPLE 1 --------------------------

    PS C:\>Get-VMToolsOnline

    This example runs the script with no parameters.  By default you will get a
    report of all available VMware Tools versions on your screen. We maintain the
    original formatting where possible.  To use the data as objects see the PassThru
    parameter in the next example.




    -------------------------- EXAMPLE 2 --------------------------

    PS C:\>$versions = Get-VMToolsOnline -PassThru

    This example saves the report to a variable.  We use the PassThru parameter which returns
    all data as objects. If we did not use PassThru, then the output is formatted using Format-Table
    which is not object friendly.




    -------------------------- EXAMPLE 3 --------------------------

    PS C:\>Get-VMToolsOnline -ShowHeader

    This example returns the default comments available on the official tools site.
    It contains helpful information about versioning, releases, etc.

    -------------------------- EXAMPLE 4 --------------------------

    PS C:\>Get-VMToolsOnline -Raw

    Returns the original content with native formatting.  This is the same thing you would see
    if you navigated to https://packages.vmware.com/tools/versions using a browser.
    
```

#### Example Output

```
PS C:\> Get-VMToolsOnline

ToolsVersion EsxVersion  ToolsRelease EsxBuild   RssAffectedTools
------------ ----------  ------------ --------   ----------------
10287        esx/0.0     10.1.15      NotBundled            False
10282        esx/0.0     10.1.10      NotBundled            False
10279        esx/6.5u1   10.1.7       5969303                True
10277        esx/6.0p05  10.1.5       5572656                True
10272        esx/6.5p01  10.1.0       5146846                True
10272        esx/6.5     10.1.0       4564106                True
10252        esx/6.5     10.0.12      4564106                True
10249        esx/5.5p11  10.0.9       6480324                True
10249        esx/5.5ep11 10.0.9       5230635                True
10249        esx/6.0u3   10.0.9       5050593                True
10249        esx/5.5p10  10.0.9       4722766                True
10249        esx/6.0p04  10.0.9       4600944                True
10249        esx/5.5p09  10.0.9       4345813                True
10249        esx/6.0p03  10.0.9       4192238                True
10249        esx/5.5p08  10.0.9       4179633                True
10248        esx/0.0     10.0.8       NotBundled             True
10246        esx/6.0u2   10.0.6       3620759                True
10245        esx/0.0     10.0.5       NotBundled             True
10240        esx/6.0ep05 10.0.0       3566359                True
10240        esx/6.0p02  10.0.0       3380124                True
10240        esx/5.5p07  10.0.0       3248547                True
10240        esx/5.5ep10 10.0.0       3568722                True
10240        esx/5.5ep09 10.0.0       3343343                True
9541         esx/6.0ep04 9.10.5       3247720                True
9541         esx/6.0u1   9.10.5       3029758                True
9537         esx/6.0p01  9.10.1       2809209                True
9536         esx/6.0     9.10.0       2494585                True
9359         esx/5.5ep08 9.4.15       3116895               False
9359         esx/5.5u3   9.4.15       3029944               False
9356         esx/5.5p05  9.4.12       2668677               False
9355         esx/5.5ep07 9.4.11       2638301               False
9355         esx/5.5ep06 9.4.11       2456374               False
9355         esx/5.5p04  9.4.11       2403361               False
9354         esx/5.5ep05 9.4.10       2143827               False
9354         esx/5.5p03  9.4.10       2143827               False
9354         esx/5.5u2   9.4.10       2068190               False
9350         esx/5.5p02  9.4.6        1892794               False
9349         esx/5.5ep04 9.4.5        1881737               False
9349         esx/5.5ep03 9.4.5        1746974               False
9349         esx/5.5ep02 9.4.5        1750340               False
9349         esx/5.5u1   9.4.5        1623387               False
9344         esx/5.5p01  9.4.0        1474528               False
9344         esx/5.5     9.4.0        1331820               False
9233         esx/5.1p09  9.0.17       3872664               False
9232         esx/5.1p08  9.0.16       3070626               False
9231         esx/5.1p07  9.0.15       2583090               False
9231         esx/5.1u3   9.0.15       2323236               False
9229         esx/5.1p06  9.0.13       2126665               False
9228         esx/5.1p05  9.0.12       1897911               False
9227         esx/5.1ep05 9.0.11       1900470               False
9227         esx/5.1p04  9.0.11       1743533               False
9226         esx/5.1ep04 9.0.10       1612806               False
9226         esx/5.1u2   9.0.10       1483097               False
9221         esx/5.1p03  9.0.5        1312873               False
9221         esx/5.1p02  9.0.5        1157734               False
9221         esx/5.1ep03 9.0.5        1117900               False
9221         esx/5.1u1   9.0.5        1065491               False
9217         esx/5.1ep02 9.0.1        1021289               False
9217         esx/5.1p01  9.0.1        914609                False
9216         esx/5.1     9.0.0        799733                False
8401         esx/5.0p13  8.6.17       3982828               False
8400         esx/5.0p12  8.6.16       3086167               False
8399         esx/5.0p11  8.6.15       2509828               False
8398         esx/5.0p10  8.6.14       2312428               False
8398         esx/5.0p09  8.6.14       1976090               False
8397         esx/5.0ep06 8.6.13       1918656               False
8397         esx/5.0p08  8.6.13       1851670               False
8396         esx/5.0p07  8.6.12       1489271               False
8395         esx/5.0u3   8.6.11       1311175               False
8395         esx/5.0p06  8.6.11       1254542               False
8395         esx/5.0ep05 8.6.11       1117897               False
8395         esx/5.0p05  8.6.11       1024429               False
8394         esx/5.0u2   8.6.10       914586                False
8397         esx/5.0p08  8.6.13       1739451               False
8389         esx/5.0p04  8.6.5        821926                False
8389         esx/5.0p03  8.6.5        768111                False
8389         esx/5.0u1   8.6.5        623860                False
8384         esx/5.0p02  8.6.0        515841                False
8384         esx/5.0p01  8.6.0        474610                False
8384         esx/5.0     8.6.0        469512                False
8307         esx/4.1p11  8.3.19                             False
8307         esx/4.1p10  8.3.19                             False
8307         esx/4.1p09  8.3.19                             False
8307         esx/4.1p08  8.3.19                             False
8306         esx/4.1p07  8.3.18                             False
8305         esx/4.1p06  8.3.17                             False
8305         esx/4.1u3   8.3.17                             False
8300         esx/4.1p05  8.3.12                             False
8300         esx/4.1p04  8.3.12                             False
8300         esx/4.1u2   8.3.12                             False
8295         esx/4.1p03  8.3.7                              False
8295         esx/4.1u1   8.3.7                              False
8290         esx/4.1     8.3.2                              False
8199         esx/4.0p15  8.0.7                              False
8199         esx/4.0p14  8.0.7                              False
8198         esx/4.0p13  8.0.6                              False
8197         esx/4.0ep09 8.0.5                              False
8196         esx/4.0p12  8.0.4                              False
8196         esx/4.0p11  8.0.4                              False
8196         esx/4.0u4   8.0.4                              False
8196         esx/4.0p10  8.0.4                              False
8196         esx/4.0u3   8.0.4                              False
8195         esx/4.0u2   8.0.3                              False
8194         esx/4.0u1   8.0.2                              False
8192         esx/4.0     8.0.0                              False
7304         esx/3.5p27  7.4.8                              False
7304         esx/3.5p25  7.4.8                              False
7304         esx/3.5p24  7.4.8                              False
7304         esx/3.5u5   7.4.8                              False
7303         esx/3.5u4   7.4.7                              False
7302         esx/3.5u3   7.4.6                              False
7302         esx/3.5u2   7.4.6                              False

```
