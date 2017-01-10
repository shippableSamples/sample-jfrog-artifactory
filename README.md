### Sample Java-Tomcat helloworld app

Demonstrates:
* Java app running on Apache Tomcat server in Docker container
* Shippable for CI
* Maven for unit tests and compilation
* Pull/deploy Java artifacts to Artifactory instance
* Push Docker images to Docker Hub
* Shippable for CD with pipeline configuration to deploy to a Test and
Prod cluster

Instructions to run this yourself:

1. Fork this repo

2. Create an account on [Shippable](http://www.shippable.com)

3. Enable your forked repo [as a project on Shippable](http://docs.shippable.com/gs_ci_sample/#enable-a-project)

4. Create Account Integrations to store your authentication credentials for third
party services
  * [Docker Hub](http://docs.shippable.com/int_docker_registries/#docker-hub)
  * [Amazon ECS](http://docs.shippable.com/int_container_services/#amazon-ec2-container-service-using-account-keys)
  * [Google GKE](http://docs.shippable.com/int_container_services/#google-container-engine-gke)

5. [Assign the integrations](http://docs.shippable.com/ci_subscriptions/#integrations)
 for use by your project for the following:
  * Your GitHub or Bitbucket integration (e.g. ttrahan-gh)
  * Your Docker Hub integration (e.g. ttrahan-dh)
  * Your Amazon ECS integration (e.g. ttrahan-aws)
  * Your Google GKE integration (e.g. ttrahan-gke)

6. Update the following in shippable.resources.yml
  * Change all integration names to match the integrations you created in 5) above
  * Change all resource locations to match your locations, e.g. change the image
  resource of type 'image' to point to your Docker Hub repo instead of 'ttrahan/javahelloworld'

7. Seed your pipeline with your configuration
  * Navigate to your subscription (select from hamburger dropdown menu in upper left)
  * Select the 'SPOG' tab
  * Select the 'Resources' tab and click 'Add Resource'
  * Select your source control integration from the list and complete remaining fields
  * NOTE: upon saving, you should see your pipeline configuration now appear on the SPOG tab

8. Create an Account Integration to link your CI runs to the image resource in
your pipeline
  * Go to Account Integrations (gear icon in upper right)
  * Select Integrations and click Add Integration
  * Select Event Trigger from the dropdown
  * Name your integration (e.g. ttrahan-trigger-javahello-pipeline)
  * Assign the integration to your subscription like in 5) above (e.g. trigger-
    javahello-pipeline)

8. Update the .m2/settings.xml file with the URL location of your Artifactory instance

9. Update the following in shippable.yml
  * The secure variable in shippable.yml with your Artifactory login password using
  the form ' PASSWORD=yourPassword '
  * The Docker Hub locations in the 'docker tag' and 'docker push' commands
  * The integrationName values under the Integrations section

10. Now commit a change to the repository
  * Your pipeline should activate and you should be able to see it execute
