Now we need to create hr backend in wordpress and use that via rest api to diaply data in front end

backend here is like this

post type name jobs where i can enter any job post with details like job type loaction job role and in house and or other platform optioj link of the posted job and now here i can name of job loaction job type like marketing tech and eployement type internship fulltime and onsite or remote and option filed like if we want to show any number how many people have already applied and now inside job and job role in conetnet editor format we can enter and

One Where i can enter all jobs and see all past jobs and now

job categories where i can create job types and then there is settings page where i can edit or update defult values or drop downs values from there

now two rest api one which list of all the jobs types with some details one which all detaisl job id and

now anothere api which like post api

where i can make post request

Fileds like name email mobile number and li keldn profile and portfolio link and some other detaisla nd pdf also store pdf media

now make one more section named application where i can list of all the applixation and some basic detaisl on click full detaisl and i can filter it by date and job post job types all those filters alo apply here

now give me php function.php code only and also add some css isnide alo for good ui also

giev em only code



code for post

```
curl -X POST 'https://yourdomain.com/wp-json/hr/v1/applications' \
-H 'Content-Type: application/json' \
-d '{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "mobile_number": "1234567890",
  "job_id": 123, // Replace with the actual Job ID
  "linkedin_profile": "https://www.linkedin.com/in/johndoe",
  "portfolio_link": "https://johndoeportfolio.com",
  "other_details": "Looking forward to joining your team.",
  "resume": "<BASE64_ENCODED_STRING>"
}'

```


now rest end points for career page




# WP Jobs API - REST Endpoints Documentation

This documentation provides an overview of the REST API endpoints available in the **WP Jobs API** plugin. These endpoints allow you to retrieve job postings and submit job applications programmatically.

---

## Endpoints Summary

1. **Jobs Endpoints** (Standard WordPress REST API)
   - **GET** `/wp-json/wp/v2/job` : Retrieve a list of job postings.
   - **GET** `/wp-json/wp/v2/job/{id}` : Retrieve a single job posting by ID.

2. **Applications Endpoint** (Custom REST API)
   - **POST** `/wp-json/hr/v1/applications` : Submit a job application.

---

## 1. Jobs Endpoints

### **GET** `/wp-json/wp/v2/job`

Retrieve a list of published job postings.

#### **Parameters**

- Standard WordPress REST API parameters are supported, such as:
  - `per_page` (integer): Number of items per page.
  - `page` (integer): Current page of the collection.
  - `search` (string): Limit results to those matching a string.
  - `job_type` (integer): Filter by Job Type taxonomy term ID.
  - `department` (integer): Filter by Department taxonomy term ID.
  - `workmode` (integer): Filter by Workmode taxonomy term ID.
  - `job_location` (integer): Filter by Job Location taxonomy term ID.

#### **Example Request**

```http
GET https://yourwebsite.com/wp-json/wp/v2/job
```

#### **Example Response**

```json
[
  {
    "id": 123,
    "date": "2023-08-01T10:00:00",
    "slug": "software-developer",
    "type": "job",
    "link": "https://yourwebsite.com/job/software-developer/",
    "title": {
      "rendered": "Software Developer"
    },
    "content": {
      "rendered": "<p>Job description goes here.</p>",
      "protected": false
    },
    "other_platform_link": "",
    "job_type": [
      {
        "id": 5,
        "name": "Full-Time",
        "slug": "full-time"
      }
    ],
    "department": [
      {
        "id": 7,
        "name": "Engineering",
        "slug": "engineering"
      }
    ],
    "workmode": [
      {
        "id": 9,
        "name": "Remote",
        "slug": "remote"
      }
    ],
    "job_location": [
      {
        "id": 11,
        "name": "New York",
        "slug": "new-york"
      }
    ],
    // ... other standard fields
  },
  // ... other job posts
]
```

---

### **GET** `/wp-json/wp/v2/job/{id}`

Retrieve a single job posting by its ID.

#### **URL Parameters**

- `{id}` (integer, required): The ID of the job post.

#### **Example Request**

```http
GET https://yourwebsite.com/wp-json/wp/v2/job/123
```

#### **Example Response**

```json
{
  "id": 123,
  "date": "2023-08-01T10:00:00",
  "slug": "software-developer",
  "type": "job",
  "link": "https://yourwebsite.com/job/software-developer/",
  "title": {
    "rendered": "Software Developer"
  },
  "content": {
    "rendered": "<p>Job description goes here.</p>",
    "protected": false
  },
  "other_platform_link": "",
  "job_type": [
    {
      "id": 5,
      "name": "Full-Time",
      "slug": "full-time"
    }
  ],
  "department": [
    {
      "id": 7,
      "name": "Engineering",
      "slug": "engineering"
    }
  ],
  "workmode": [
    {
      "id": 9,
      "name": "Remote",
      "slug": "remote"
    }
  ],
  "job_location": [
    {
      "id": 11,
      "name": "New York",
      "slug": "new-york"
    }
  ],
  // ... other standard fields
}
```

#### **Additional Notes**

- The response includes custom fields:
  - `other_platform_link`: A URL if the job is posted on another platform; otherwise, an empty string.
- Taxonomy terms are provided for:
  - `job_type`
  - `department`
  - `workmode`
  - `job_location`

---

## 2. Applications Endpoint

### **POST** `/wp-json/hr/v1/applications`

Submit a new job application.

#### **Request Headers**

- `Content-Type`: `application/json`

#### **Request Body Parameters**

- **name** (string, required): Applicant's full name.
- **email** (string, required): Applicant's email address.
- **mobile_number** (string, required): Applicant's mobile number.
- **job_id** (integer, required): The ID of the job being applied for.
- **linkedin_profile** (string, optional): URL to the applicant's LinkedIn profile.
- **portfolio_link** (string, optional): URL to the applicant's portfolio or website.
- **current_ctc** (string, optional): Current Cost to Company.
- **expected_ctc** (string, optional): Expected Cost to Company.
- **notice_period** (string, optional): Notice period duration.
- **resume** (string, optional): Base64-encoded resume file content (PDF, DOC, or DOCX formats).

#### **Example Request**

```http
POST https://yourwebsite.com/wp-json/hr/v1/applications
Content-Type: application/json

{
  "name": "Jane Doe",
  "email": "jane.doe@example.com",
  "mobile_number": "+1234567890",
  "job_id": 123,
  "linkedin_profile": "https://linkedin.com/in/janedoe",
  "portfolio_link": "https://janedoeportfolio.com",
  "current_ctc": "50,000 USD",
  "expected_ctc": "60,000 USD",
  "notice_period": "1 month",
  "resume": "base64-encoded-resume-content"
}
```

#### **Example Successful Response**

```json
{
  "status": "success",
  "application_id": 456
}
```

#### **Error Responses**

- **400 Bad Request**: Missing required fields or invalid data.

  ```json
  {
    "code": "missing_fields",
    "message": "Required fields are missing.",
    "data": {
      "status": 400
    }
  }
  ```

- **500 Internal Server Error**: Application submission failed due to server error.

  ```json
  {
    "code": "insert_failed",
    "message": "Application submission failed.",
    "data": {
      "status": 500
    }
  }
  ```

#### **Notes**

- The `resume` parameter must be a base64-encoded string of the file content.
- Accepted resume file formats are PDF (`.pdf`), Microsoft Word Document (`.doc`), and Word Open XML Document (`.docx`).
- On successful submission, a confirmation email is sent to the applicant.

---

## Authentication & Permissions

- **Jobs Endpoints**: Publicly accessible; no authentication required.
- **Applications Endpoint**: Publicly accessible for submissions; no authentication required.

---

## Additional Information

### **Retrieving Jobs with Filters**

You can filter job listings using taxonomy term IDs.

#### **Example: Retrieve Jobs in the Engineering Department**

```http
GET https://yourwebsite.com/wp-json/wp/v2/job?department=7
```

#### **Example: Retrieve Remote Full-Time Jobs**

```http
GET https://yourwebsite.com/wp-json/wp/v2/job?workmode=9&job_type=5
```

---

## Usage Tips

- **Pagination**: Use `per_page` and `page` parameters to handle large sets of job postings.
- **Searching**: Use the `search` parameter to find jobs matching specific keywords.
- **Handling Responses**: Always check for HTTP status codes and handle error messages gracefully in your application.

---

## Common Use Cases

### **1. Displaying Job Listings on a Website**

Fetch job postings and display them on your website's careers page.

```http
GET https://yourwebsite.com/wp-json/wp/v2/job?per_page=10
```

### **2. Job Application Submission Form**

Create a frontend form that collects applicant information and submits it via the Applications endpoint.

- Collect all required fields (`name`, `email`, `mobile_number`, `job_id`).
- Optionally, include fields for LinkedIn profile, portfolio link, current/expected CTC, notice period, and resume upload.
- Convert the uploaded resume file to a base64-encoded string before submission.

---

## Important Notes

- **Data Validation**: Ensure all required fields are provided and valid before making API requests.
- **File Size Limits**: Be mindful of server limits on file upload sizes when submitting resumes.
- **Security**: Since the Applications endpoint is publicly accessible, implement client-side validation to prevent abuse.

---

## Contact & Support

If you encounter any issues or have questions about using the WP Jobs API plugin, please reach out to the plugin author or consult the plugin's support resources.

---

## Conclusion

The WP Jobs API plugin provides a simple and efficient way to interact with job postings and applications via REST API endpoints. Whether you're building a custom careers page or integrating with third-party services, these endpoints allow for flexible and dynamic solutions.

---

Feel free to reach out if you need further assistance or have any questions about using these endpoints!


