# Site template

Can copy and paste this site template, and personalize:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/DECORATION/1.8.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/DECORATION/1.8.0 http://maven.apache.org/xsd/decoration-1.8.0.xsd"
	name="${project.name}">
	<publishDate position="bottom" format="dd-MM-yyy" />
	<version position="bottom" />
	<skin>
		<groupId>org.joda.external</groupId>
		<artifactId>reflow-maven-skin</artifactId>
		<version>1.2</version>
	</skin>

	<custom>
		<reflowSkin>
			<!-- Reflow configuration See http://andriusvelykis.github.io/reflow-maven-skin/skin/config.html -->
			<theme>bootswatch-spruce</theme>
			<highlightJs>true</highlightJs>
			<skinAttribution>false</skinAttribution>
			<brand>
				<name>${project.name}</name>
				<href>index.html</href>
			</brand>
			<topNav>Info and Reports</topNav> <!-- Add other menu name here, with regex: Documentation|Info and Reports|Another menu... -->
			<bottomNav>
				<column>Code</column>
				<column>Releases</column>
			</bottomNav>
			<bottomDescription><![CDATA[
        ${project.description}
      ]]></bottomDescription>
			<toc>false</toc>
			<breadcrumbs>false</breadcrumbs>
			<markPageHeader>false</markPageHeader>
			<protocolRelativeURLs>true</protocolRelativeURLs>
			<pages>
				<index>
					<sections>
						<columns>2</columns>
						<body />
						<sidebar />
					</sections>
					<shortTitle>Home</shortTitle>
					<highlightJs>true</highlightJs>
				</index>
				<!-- Other pages here: <page_name> <sections> ... </page_name> See http://andriusvelykis.github.io/reflow-maven-skin/skin/layouts.html -->
			</pages>
		</reflowSkin>
	</custom>

	<body>
		<head>
			<![CDATA[<link rel="icon" type="image/png" href="images/logo-albirar-icon.png"></link>]]>
		</head>
		<menu name="Info and Reports" inherit="top"
			alt="Info and Reports" title="Info and Reports">
			<item name="Info" href="project-info.html" />
			<item name="Reports" href="project-reports.html" />
			<item name="JavaDocs" href="apidocs/" />
		</menu>
		<menu name="Code" inherit="top" alt="Code" title="Code">
			<item name="Source Code" href="${project.scm.url}" alt="Github"
				title="Github" img="images/GitHub-Mark-32px.png">
				<description>GitHub</description>
			</item>
			<item name="CI" href="${project.ciManagement.url}"
				alt="${project.ciManagement.system}"
				title="${project.ciManagement.system}" img="images/TravisCI-32px.png">
				<description>${project.ciManagement.system}</description>
			</item>
			<item name="Issues" href="${project.issueManagement.url}"
				alt="${project.issueManagement.system} Issues"
				title="${project.issueManagement.system} Issues"
				img="images/Octocat-32px.png">
				<description>${project.issueManagement.system} Issues</description>
			</item>
		</menu>
		<menu name="Releases" inherit="top" alt="Releases"
			title="Releases">
			<item name="Maven Central" alt="Maven Central"
				title="Maven Central"
				img="images/maven-logo-black-on-white-32px.png"
				href="https://search.maven.org/artifact/${project.groupId}/${project.artifactId}" />
		</menu>
	</body>
</project>
```