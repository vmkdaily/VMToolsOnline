NAME
    Get-VMToolsOnline

SYNOPSIS
    Uses Powershell webcmdlets to connect to vmware.com and get a list of all
    VMware Tools versions along with supporting infgormation.


SYNTAX
    Get-VMToolsOnline [-Uri <String>] [-PassThru] [<CommonParameters>]

    Get-VMToolsOnline [-ShowHeader] [<CommonParameters>]

    Get-VMToolsOnline [-Raw] [<CommonParameters>]


DESCRIPTION
    Uses Powershell webcmdlets to connect to vmware.com and get a list of all
    VMware Tools versions along with supporting infgormation.  Also includes
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
    report of all available VMware Tools versions on your screen. WE maintain the
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


