---
layout: default
title: .NET Tool Anatomy Cheat Sheet
---

<div class="coversheet">
  <h1><span class="icon">&#x1F6E0;</span> .NET Tool Anatomy Cheat Sheet</h1>
  <p>A quick-reference guide to building, distributing, and publishing command-line tools with the .NET CLI</p>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4D8;</span> Getting Started</h2>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">A .NET tool is a self-contained executable you install and invoke via <code>dotnet &lt;tool&gt;</code>. Think <code>dotnet ef</code>, <code>dotnet new</code> extensions, or <code>dotnet-coverage</code>.</p>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F527;</span> Step 1: Create the Project</h3>
    <p>Scaffold a new tool project:</p>
    <pre><code>dotnet new console -n MyCliTool
cd MyCliTool</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4DC;</span> Step 2: Mark as a Tool Package</h3>
    <p>Add the <code>&lt;PackAsTool&gt;</code> property to your .csproj:</p>
    <pre><code>&lt;PropertyGroup&gt;
  &lt;OutputType&gt;Exe&lt;/OutputType&gt;
  &lt;TargetFramework&gt;net8.0&lt;/TargetFramework&gt;
  &lt;PackAsTool&gt;true&lt;/PackAsTool&gt;
  &lt;ToolCommandName&gt;mytool&lt;/ToolCommandName&gt;
&lt;/PropertyGroup&gt;</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x2699;&#xFE0F;</span> Step 3: Write the Entrypoint</h3>
    <p>Your <code>Program.cs</code> is the CLI entrypoint:</p>
    <pre><code>using System.CommandLine;

var rootCommand = new RootCommand("My CLI tool")
{
    new Option&lt;string&gt;(new[] { "--name", "-n" }, "Name to greet"),
};

rootCommand.SetHandler(name =>
{
    Console.WriteLine($"Hello, {name}!");
});

return await rootCommand.InvokeAsync(args);</code></pre>
  </div>
</div>

<div class="note"><strong>Tip:</strong> Use <a href="https://github.com/dotnet/command-line-api">System.CommandLine</a> for argument parsing — it is the officially recommended library and handles help text, versioning, and error output automatically.</div>

<h2 class="section-heading"><span class="icon">&#x1F50E;</span> Anatomy of a Tool Package</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4D6;</span> .csproj (Package Manifest)</h3>
    <p>The critical .csproj for a tool:</p>
    <pre><code>&lt;Project Sdk="Microsoft.NET.Sdk"&gt;

  &lt;PropertyGroup&gt;
    &lt;OutputType&gt;Exe&lt;/OutputType&gt;
    &lt;TargetFramework&gt;net8.0&lt;/TargetFramework&gt;
    &lt;PackAsTool&gt;true&lt;/PackAsTool&gt;
    &lt;ToolCommandName&gt;mytool&lt;/ToolCommandName&gt;
    &lt;PackageOutputHost&gt;https://api.nuget.org&lt;/PackageOutputHost&gt;
  &lt;/PropertyGroup&gt;

  &lt;ItemGroup&gt;
    &lt;PackageReference
      Include="System.CommandLine"
      Version="2.0.0-beta4.22272.1" /&gt;
  &lt;/ItemGroup&gt;

&lt;/Project&gt;</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F510;</span> Key MSBuild Properties</h3>
    <ul>
      <li><code>&lt;PackAsTool&gt;true&lt;/PackAsTool&gt;</code> — marks the package as installable via <code>dotnet tool install</code></li>
      <li><code>&lt;ToolCommandName&gt;mytool&lt;/ToolCommandName&gt;</code> — name used to invoke (<code>dotnet mytool</code>)</li>
      <li><code>&lt;OutputType&gt;Exe&lt;/OutputType&gt;</code> — must be an executable, not a library</li>
      <li><code>&lt;PackageVersion&gt;</code> — NuGet version (required for publishing)</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E6;</span> Program.cs (Entry Point)</h3>
    <p>The <code>Main</code> method is what runs when a user invokes the tool:</p>
    <pre><code>static int Main(string[] args)
{
    // 1. Define options &amp; arguments
    // 2. Wire up handlers
    // 3. Invoke the command line parser
    return exitCode;
}</code></pre>
    <p>Return an <code>int</code> exit code — non-zero signals error.</p>
  </div>
</div>

<div class="card-standalone">
  <h2 class="section-heading"><span class="icon">&#x1F4CB;</span> Package Manifest (nuget.spec)</h2>
  <p>Beyond <code>PackAsTool</code>, these metadata fields are required for NuGet publishing:</p>
  <pre><code>&lt;PropertyGroup&gt;
  &lt;Id&gt;MyOrg.MyCliTool&lt;/Id&gt;
  &lt;Title&gt;My CLI Tool&lt;/Title&gt;
  &lt;Authors&gt;Your Name&lt;/Authors&gt;
  &lt;Version&gt;1.0.0&lt;/Version&gt;
  &lt;Description&gt;A short description of the tool.&lt;/Description&gt;
  &lt;ProjectUrl&gt;https://github.com/you/repo&lt;/ProjectUrl&gt;
  &lt;RepositoryUrl&gt;https://github.com/you/repo&lt;/RepositoryUrl&gt;
  &lt;PackageProjectUrl&gt;https://github.com/you/repo&lt;/PackageProjectUrl&gt;
  &lt;PackageLicenseExpression&gt;MIT&lt;/PackageLicenseExpression&gt;
  &lt;PackageReadmeFile&gt;README.md&lt;/PackageReadmeFile&gt;
  &lt;PackageTags&gt;cli;tool;dotnet&lt;/PackageTags&gt;
&lt;/PropertyGroup&gt;

&lt;ItemGroup&gt;
  &lt;None Include="..\README.md" Pack="true"
    PackagePath="\" /&gt;
&lt;/ItemGroup&gt;</code></pre>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4E6;</span> Installing &amp; Using Your Tool</h2>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">From the perspective of someone consuming a published .NET tool:</p>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4E2;</span> Install Globally</h3>
    <pre><code>dotnet tool install --global MyCliTool</code></pre>
    <p>Then invoke anywhere:</p>
    <pre><code>dotnet mytool --name World</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4CB;</span> Install Locally (manifold)</h3>
    <pre><code>dotnet new tool-manifest
dotnet tool install MyCliTool</code></pre>
    <p>Stored in <code>.config/dotnet-tools.json</code> — scoped to the repo.</p>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F468;&#x200D;&#x1F4BB;</span> Use Without Installing</h3>
    <pre><code>dotnet tool run MyCliTool --name World</code></pre>
    <p>Ignores installed tools — always uses the latest NuGet version.</p>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F504;</span> Update / Uninstall</h3>
    <pre><code># Update to latest version
dotnet tool update --global MyCliTool

# Uninstall
dotnet tool uninstall --global MyCliTool

# List installed tools
dotnet tool list --global</code></pre>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4E4;</span> Publishing the Tool</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F528;</span> Step 1: Pack the Nupkg</h3>
    <p>Create the NuGet package locally:</p>
    <pre><code>dotnet pack -c Release</code></pre>
    <p>This produces <code>bin/Release/MyCliTool.1.0.0.nupkg</code>. Verify contents:</p>
    <pre><code>unzip -l bin/Release/MyCliTool.1.0.0.nupkg | grep .dll</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x2601;&#xFE0F;</span> Step 2: Push to NuGet.org</h3>
    <pre><code># First, verify the package will succeed (dry run)
nuget push bin/Release/MyCliTool.1.0.0.nupkg \
  -k $NUGET_API_KEY \
  -s https://api.nuget.org/v3/index.json

# Or use the dotnet CLI:
dotnet nuget push bin/Release/MyCliTool.1.0.0.nupkg \
  --api-key $NUGET_API_KEY \
  --source https://api.nuget.org/v3/index.json</code></pre>
    <p><code>$NUGET_API_KEY</code> is your NuGet.org API key (manage at <code>nuget.org/profile</code>).</p>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x2699;&#xFE0F;</span> Step 3: CI/CD Automation</h3>
    <pre><code># GitHub Actions example
- name: Pack &amp; publish
  run: |
    dotnet pack -c Release
    dotnet nuget push **/*.nupkg \
      --api-key ${{ secrets.NUGET_KEY }} \
      --source https://api.nuget.org/v3/index.json
    --skip-duplicate</code></pre>
  </div>
</div>

<div class="warning-box"><strong>Warning:</strong> Once published, you <strong>cannot overwrite</strong> a NuGet package version. To fix a broken release, bump the version number and publish again.</div>

<h2 class="section-heading"><span class="icon">&#x1F4E3;</span> Debugging &amp; Development Tips</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F50D;</span> Local Dev Loop</h3>
    <pre><code># Create a tool-manifest in your test project
dotnet new tool-manifest

# Reference your local tool
dotnet tool add --local MyCliTool --prerelease \
  --source ./src/MyCliTool/bin/Debug/

# Now `dotnet mytool` runs the local build</code></pre>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4A1;</span> Common Issues &amp; Fixes</h3>
    <ul>
      <li><strong>"Command not found"</strong> — verify <code>&lt;ToolCommandName&gt;</code> matches what you typed</li>
      <li><strong>"Could not find a manifest file"</strong> — run <code>dotnet new tool-manifest</code> first</li>
      <li><strong>"Package not found"</strong> — check <code>--source</code> or publish to your feed first</li>
      <li><strong>"Unable to resolve framework"</strong> — ensure <code>&lt;TargetFramework&gt;</code> matches installed SDK</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F524;</span> Multi-Framework Support</h3>
    <pre><code>&lt;TargetFrameworks&gt;net8.0;net6.0;&lt;/TargetFrameworks&gt;</code></pre>
    <p>Tools must specify at least one TFM. Multi-targeting is fine but the package file name uses the first target framework by default.</p>
  </div>
</div>

<div class="mini-grid">
  <div class="mini-item">Use <code>--prerelease</code> flag when testing with pre-release versions</div>
  <div class="mini-item"><code>dotnet tool list --global</code> shows all globally installed tools</div>
  <div class="mini-item">Tools can be built on any OS — they ship as cross-platform .dlls + shim executors</div>
  <div class="mini-item">Use <code>.targets</code> files for SDK-style tool distribution beyond NuGet</div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4C8;</span> Tool Invocation Flow</h2>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">What happens under the hood when you run <code>dotnet mytool --help</code>:</p>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x25B6;&#xFE0F;</span> Resolution Steps</h3>
    <ol>
      <li>CLI checks for local manifest (<code>.config/dotnet-tools.json</code>)</li>
      <li>Falls back to global tool registry (~/.dotnet/tools)</li>
      <li>Resolves the package from NuGet feeds if not found</li>
      <li>Creates a shim executable that invokes <code>dotnet &lt;tool&gt;</code></li>
      <li>Routes arguments to your <code>Main(string[] args)</code></li>
    </ol>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4C2;</span> Tool Shims</h3>
    <p>Installed tools live as "shims" (wrappers):</p>
    <ul>
      <li><strong>Global:</strong> ~/.dotnet/tools/</li>
      <li><strong>Local:</strong> .config/dotnet-tools.json</li>
      <li>The shim is just an executable that forwards to the NuGet package</li>
      <li>You can edit the shim script for custom behavior</li>
    </ul>
  </div>
</div>

<div class="card-grid" style="margin-bottom: 1rem;">
  <div class="card-item">
    <div class="tip-box"><strong>Tip:</strong> Use <code>dotnet tool update --global mytool --prerelease</code> to preview the latest unstable build without changing your project files.</div>
  </div>
  <div class="card-item">
    <div class="warning-box"><strong>Warning:</strong> The <code>&lt;ToolCommandName&gt;</code> defaults to the package name minus the "dotnet." prefix — so <code>dotnet-coverage</code> stays as-is.</div>
  </div>
</div>

<p class="credits">Made with <span style="color: var(--accent-pink);">&#x2764;</span> for developers &mdash; keep building! &#x1F680;</p>
