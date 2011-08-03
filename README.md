# GitHub Maven Plugins
Collection of [Maven](http://maven.apache.org/) plugins that integrate with GitHub

## Downloads Plugin
Maven plugin that creates and uploads a built resource to be available as a
GitHub repository download.  The plugin is bound to the `upload` goal.

### Configuration
The downloads plugin supports several configuration options that can either
be expressed in your project's POM file or in your settings.xml file.  Where
you put the downloads-plugin settings depends on whether you want a specific
setting to be configured globally or on a per-project basis.

The notation belows shows the plugin configuration property name followed
by the settings configuration property in `()`.

* host (github.downloads.host)
  * Domain of GitHub API calls (defaults to `api.github.com`)
* oauth2Token (github.downloads.oauth2token)
  * OAuth2 access token for API authentication
  * [More about GitHub OAuth support](http://developer.github.com/v3/oauth/)
* userName (github.downloads.userName)
  * GitHub user name used for API authentication
* password (github.downloads.password)
  * GitHub password used for API authentication
* description
  * Description visible on the repository download page
* includes
  * Sub-elements will be treated as patterns to include from the `{project.build.directory` as downloads
* excludes
  * Sub-elements will be treated as patterns to exclude from the `{project.build.directory` as downloads
* override (github.downloads.override)
  * true|false (default: false)
  * Whether existing downloads with the same name will be deleted before attempting to upload a new version
  * *Note:* Attempts to upload a download with the same name as one that already exists will fail unless this is set to true
* repositoryName
  * Name of repository that downloads will be uploaded to
* repositoryOwner
  * Owner of repository that downloads will be uploaded to

*Note:* `repositoryOwner` property and `repositoryName` are optional and will be inferred from the following properties if not specified

 * `project.url`
 * `project.scm.url`
 * `project.scm.connection`
 * `project.scm.developerConnection`

### Example
```xml
<build>
  <plugins>
    <plugin>
      <groupId>com.github.maven.plugins</groupId>
      <artifactId>github-downloads-plugins</artifactId>
      <executions>
        <execution>
          <configuration>
            <description>Official build of the ${project.version} release</description>
            <override>true</override>
            <excludes>
              <exclude>**/unit-tests.jar</exclude>
            </excludes>
            <includes>
              <include>**/*.jar</include>
            </includes>
          </configuration>
          <goals>
            <goal>upload</goal>
          </goals>
          <phase>install</phase>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

#License
* [MIT License](http://www.opensource.org/licenses/mit-license.php)
