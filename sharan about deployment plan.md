Deployment

Integration build OCD and build - coming over the doors-http
Look over some other deployment plans
Upload the videos from discussion with rob

Done


1. Migrate db to production
2. Check with brad that the updates that were made
3. API key created with the policy defined
4.  22208e7bc0a88387ef5c766f48909273472bc3b7
5. Make an API call from postman


Steps for macygrey
1. Migrated macygrey database tables from dev to production
2. Deployed latest version to production cluster using the pipeline
3. Created API-key for methods
4. Made request using the API-Keys.

Steps for OCD
1. Added queue for case where the list is modified from macygrey
2. Spun down dev OCD and macygrey to prevent the wrong OCD to consuming the queue.
3. Ran macygrey and OCD locally.
4. Attached break point to getGreyList() method.
5. Set and delete methods in macygrey triggered OCD event RMQ broker

Steps for build
1. TBD

Production image on AWS
164522539201.dkr.ecr.ap-southeast-2.amazonaws.com/nl-macygrey:1.0.0 
