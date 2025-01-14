# Artifact Repository Management with Nexus


## 1. What is Nexus?

Nexus Repository Manager is a powerful tool that allows you to store, manage, and retrieve build artifacts. It supports various formats including Maven, Docker, npm, and more. Nexus can function as a proxy for public repositories, reducing download times and saving bandwidth by caching artifacts locally.

## 2. Installation of Nexus

### Prerequisites

- Java Development Kit (JDK) installed on your machine.
- Access to a terminal or command prompt.

### Steps to Install

1. **Download Nexus**: From terminal downlaod the source tar file into the `/opt` folder and extract it.
```
wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
```
2. **Extract the Archive**: Unzip the downloaded file to your desired installation directory.
```
tar -xvzf latest-unix.tar.gz
```
3. **Create a new user for nexus only**
```
adduser nexus
```
4. **Assign this user for nexus app folders**
```
chown -R nexus:nexus sonatype-work/ nexus-3.76.0-03/
```
5. **Set the configuration to use nexus as the user**

```
vim nexus-3.76.0-03/bin/nexus.rc 
```

set the code below: 
```
run_as_user="nexus"
```
6. **Switch to nexus user**
```
sudo - nexus
```

7. **Start Nexus**:
   - Navigate to the `nexus` directory in your terminal.
   - Run the following command:
     ```
     /opt/nexus-3.76.0-03/bin/nexus start
     ```
4. **Accessing Nexus**: Open your web browser and go to `http://localhost:8081/`.


## 3. Configuring Nexus

### Default User Credentials

- **Username**: `admin`
- **Password**: `admin123`

After logging in, change your password for security purposes.

### Repository Types

Nexus supports three types of repositories:

- **Hosted Repositories**: For storing your own artifacts.
- **Proxy Repositories**: For caching artifacts from remote repositories.
- **Group Repositories**: To aggregate multiple repositories into one URL.

## 4. Creating a Repository

### Steps to Create a Repository

1. **Log in to Nexus** at `http://localhost:8081/nexus/`.
2. Click on **Repositories** in the left sidebar.
3. Click on the **Create repository** button.
4. Choose the type of repository you want to create (e.g., Maven2 hosted).
5. Fill in the required fields:
   - **Name**: A unique name for your repository.
   - **Blob Store**: Select or create a blob store where artifacts will be stored.
6. Click on **Create repository**.

## 5. Managing Artifacts

### Deploying Artifacts

To deploy an artifact:

1. Use the following command with Maven:
```
mvn deploy:deploy-file -DgroupId=com.example
-DartifactId=my-artifact
-Dversion=1.0
-Dpackaging=jar
-Dfile=path/to/my-artifact.jar
-DrepositoryId=nexus-repo
-Durl=http://localhost:8081/nexus/repository/my-repo/
```



### Retrieving Artifacts

You can retrieve artifacts from Nexus using Maven or other build tools by specifying the repository URL in your project’s configuration file (e.g., `pom.xml` for Maven).

## 6. Integrating with CI/CD Tools

Nexus integrates seamlessly with CI/CD tools like Jenkins, Bamboo, and TeamCity:

- Configure your CI/CD tool to use Nexus as a repository for dependencies and artifacts.
- Set up build jobs to publish artifacts to Nexus upon successful builds.

## 7. Monitoring and Maintenance

Regularly monitor your Nexus instance for performance issues and perform maintenance tasks such as:

- Cleaning up unused artifacts.
- Backing up your repository data.
- Upgrading Nexus to the latest version for new features and security updates.

---


