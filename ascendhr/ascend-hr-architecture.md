# AscendHR Product Architecture & Infrastructure

**Document Version:** 1.0  
**Last Updated:** January 7, 2026  
**Prepared For:** Executive Leadership (CEO, CTO)  
**Status:** Production

---

## Executive Summary

AscendHR is a modern, cloud-native HR Management System built on a serverless architecture using AWS services. The platform provides comprehensive employee management, performance tracking, leave management, and organizational structure visualization capabilities.

**Key Highlights:**
- **100% Serverless Architecture** - Zero server management overhead
- **Cost-Effective** - Estimated $2-3/month for 100 daily active users
- **Highly Scalable** - Auto-scales from 1 to 10,000+ users without infrastructure changes
- **Modern Tech Stack** - React 19, TypeScript, AWS Lambda, DynamoDB
- **Region:** Asia Pacific (Singapore) - ap-southeast-1
- **Deployment:** Fully automated CI/CD via Bitbucket Pipelines


## Technology Stack

### Frontend Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **React** | 18.3.1 | UI framework with modern hooks |
| **TypeScript** | 5.8.3 | Type-safe development |
| **Vite** | 5.4.19 | Fast build tool and dev server |
| **TailwindCSS** | 3.4.17 | Utility-first CSS framework |
| **Radix UI** | Latest | Accessible component primitives (shadcn/ui) |
| **React Router** | 6.30.1 | Client-side routing |
| **TanStack Query** | 5.83.0 | Server state management & caching |
| **React Hook Form** | 7.61.1 | Form handling |
| **Zod** | 3.25.76 | Schema validation |
| **Recharts** | 2.15.4 | Data visualization |
| **Lucide React** | 0.462.0 | Icon library |

### Backend Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **Node.js (HONO)** | 20.x | Runtime environment |
| **SST (Serverless Stack)** | 3.5.0 | Infrastructure as Code framework |
| **AWS Lambda** | Node.js 20.x | Serverless compute |
| **Dynamoose** | 4.0.1 | DynamoDB ORM |
| **AWS SDK v3** | 3.600.0+ | AWS service integration |

### Development Tools

| Tool | Purpose |
|------|---------|
| **pnpm** | Package manager with workspaces |
| **Turbo** | Monorepo build orchestration |
| **Bitbucket Pipelines** | CI/CD automation |

---

## Infrastructure Architecture

### Architecture Diagram (Logical View)

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                             │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │   Web Browser (React SPA)                                   │ │
│  └────────────────────────────────────────────────────────────┘ │
└───────────────────────────┬─────────────────────────────────────┘
                            │ HTTPS
┌───────────────────────────▼─────────────────────────────────────┐
│                    AWS AMPLIFY HOSTING                           │
│  • CloudFront CDN Distribution (Global)                          │
│  • Static Asset Hosting (SPA)                                    │
│  • SSL/TLS Certificates                                          │
│  • CI/CD Build Pipeline                                          │
└───────────────────────────┬─────────────────────────────────────┘
                            │ API Calls
┌───────────────────────────▼─────────────────────────────────────┐
│                  AWS API GATEWAY (HTTP API)                       │
│  • RESTful HTTP endpoints                                        │
│  • Request routing & throttling                                  │
│  • CORS configuration                                            │
│  • Request/Response transformation                               │
└───┬─────────────┬─────────────┬─────────────┬──────────────────┘
    │             │             │             │
    ▼             ▼             ▼             ▼
┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐
│ Lambda  │  │ Lambda  │  │ Lambda  │  │ Lambda  │  ... (6 total)
│  Auth   │  │Employee │  │  Leave  │  │  Org    │
└────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘
     │            │             │             │
     └────────────┴─────────────┴─────────────┘
                  │
     ┌────────────┴────────────┬
     │                         │                
     ▼                         ▼                
┌─────────────────┐  ┌──────────────────┐  
│   DYNAMODB      │  │  AWS S3 BUCKET   │  │   │
│  (9 Tables)     │  │  (File Storage)  │  │  │
│  • employees    │  │  • Avatars       │  │       │
│  • users        │  │  • Documents     │  │            │
│  • departments  │  │                  │  │            │
│  • positions    │  │                  │  │            │
│  • leave-req    │  │                  │  │            │
│  • announce     │  │                  │  │            │
│  • attributes   │  │                  │  │            │
│  • squads       │  │                  │  │            │
│  • orgs         │  │                  │  │            │
└─────────────────┘  └──────────────────┘  └────────────┘
         │
         ▼
┌─────────────────┐
│   CLOUDWATCH    │
│  • Logs         │
│  • Metrics      │
│  • Alarms       │
└─────────────────┘
```
---

## AWS Services Breakdown

### 1. AWS Amplify Hosting

**Purpose:** Frontend web application hosting and deployment

**Configuration:**
- **Build System:** Node.js 20 with pnpm
- **Build Command:** `pnpm run build`
- **Output Directory:** `dist/`
- **CDN:** CloudFront distribution included
- **SSL:** Automatic SSL certificates
- **Environment:** Static SPA hosting

**Features Used:**
- Automatic builds from Git commits
- Environment variable management
- Instant cache invalidation
- Global CDN distribution
- Custom domain support

**Why We Chose It:**
- Seamless integration with AWS ecosystem
- Zero-config SSL and CDN
- Automatic deployments on Git push
- Cost-effective for static sites
- Built-in performance optimizations

---

### 2. AWS Lambda

**Purpose:** Serverless compute for backend API logic

**Configuration:**
- **Runtime:** Node.js 20.x (Hono)
- **Architecture:** x86_64
- **Memory:** 512 MB (configurable per function)
- **Timeout:** 30 seconds (API Gateway limit)
- **Concurrency:** Auto-scaling (no reserved capacity)

**Why We Chose Lambda:**
- Zero infrastructure management
- Automatic scaling (0 to millions of requests)
- Pay-per-execution model (cost-effective at low volume)
- Built-in high availability
- Fast cold start times with Node.js 20

---

### 3. Amazon API Gateway V2 (HTTP API)

**Purpose:** HTTP API gateway for routing requests to Lambda functions

**Configuration:**
- **API Type:** HTTP API (not REST API - 70% cheaper)
- **Protocol:** HTTPS only
- **CORS:** Enabled for frontend domain
- **Authorization:** JWT-based (handled in Lambda)
- **Throttling:** AWS default limits

**Why We Chose HTTP API (vs REST API):**
- 70% cheaper than REST API Gateway
- Lower latency
- Built-in JWT authorizers
- Simpler configuration
- Sufficient features for our use case

---

### 4. Amazon DynamoDB

**Purpose:** NoSQL database for all application data

**Data Model Highlights:**
- Denormalized for read performance
- Attribution scores embedded in employee records
- Historical performance tracking with change logs
- Rich metadata for reporting

**Why We Chose DynamoDB:**
- Fully managed (no patching, backups automatic)
- Single-digit millisecond latency
- Virtually unlimited scalability
- On-demand pricing fits usage pattern
- Strong consistency available when needed
- Excellent AWS Lambda integration

---

### 5. Amazon S3

**Purpose:** Object storage for user-uploaded files

**Use Cases:**
- Employee profile avatars
- Document uploads (resumes, certifications)
- Organization logos
- Report exports (PDF, Excel)

**Access Pattern:**
- Frontend requests presigned URLs from Lambda
- Direct browser upload/download via presigned URLs
- No direct public access (security)


**Why We Chose S3:**
- Industry standard for object storage
- 99.999999999% (11 9's) durability
- Presigned URLs for secure direct uploads
- Pay only for storage used
- Integrates with CloudFront for CDN delivery

---

### 6. Amazon CloudWatch

**Purpose:** Monitoring, logging, and observability

**Components Used:**

**CloudWatch Logs:**
- All Lambda function logs automatically captured
- Log retention: 7 days default
- Log groups per Lambda function
- Searchable and filterable

**CloudWatch Metrics:**
- Lambda invocations, duration, errors
- API Gateway requests, latency, errors
- DynamoDB read/write capacity, throttles
- Automatic AWS service metrics

**Monitoring Capabilities:**
- Real-time function execution logs
- Error tracking and debugging
- Performance metrics and trends
- Configurable alarms (not yet configured)

**Why It's Essential:**
- Automatic log collection (no setup needed)
- Centralized logging for all services
- Performance troubleshooting
- Security audit trails
- Free tier covers current usage

---

## Cost Analysis (100 Daily Active Users)

### Assumptions

**User Activity Profile:**
- **Daily Active Users (DAU):** 100
- **Monthly Active Users (MAU):** ~120 (accounting for weekends/holidays)
- **Average API Calls per User per Day:** 75 calls
  - 40 GET requests (viewing data)
  - 25 POST/PATCH requests (data entry)
  - 10 DELETE requests (occasional)
- **Active Days per Month:** 30

**Calculated Monthly Volumes:**
- **Total API Calls:** 100 users × 75 calls × 30 days = **225,000 calls/month**
- **Lambda Invocations:** 225,000 (1:1 with API calls)
- **Average Lambda Execution Time:** 200ms
- **Average Lambda Memory:** 512 MB
- **DynamoDB Operations:**
  - Read operations: 135,000/month (60% of calls)
  - Write operations: 90,000/month (40% of calls)
- **Data Storage:**
  - DynamoDB: ~1 GB (employee data, relationships)
  - S3: ~0.5 GB (100 users × 5 MB average files)
- **Data Transfer Out:** ~10 GB/month
- **Monthly Builds:** 4 builds (weekly deployments)

---

### Detailed Cost Breakdown

#### 1. AWS Lambda - $0.00/month

**Free Tier (Permanent):**
- 1,000,000 requests per month
- 400,000 GB-seconds of compute time per month

**Usage:**
- Requests: 225,000 (22.5% of free tier)
- Compute: 225,000 invocations × 0.2s × 0.5 GB = 22,500 GB-seconds (5.6% of free tier)

**Status:** ✅ **Entirely within free tier**

---

#### 2. API Gateway HTTP API - $0.00/month (Year 1) | $0.23/month (Year 2+)

**Free Tier (First 12 Months):**
- 1,000,000 API calls per month

**Usage:**
- API Calls: 225,000/month

**Pricing After Free Tier:**
- First 300M requests: $1.00 per million
- 225,000 requests × $1.00 / 1,000,000 = **$0.23/month**

**Status:** ✅ **Free for first year**, minimal cost after

---

#### 3. DynamoDB On-Demand - $0.39/month

**Pricing (ap-southeast-1):**
- Write Request Units: $1.25 per million
- Read Request Units: $0.25 per million
- Storage (Standard): $0.25 per GB-month

**Usage & Cost:**
- **Write Requests:** 90,000 × $1.25 / 1,000,000 = **$0.11/month**
- **Read Requests:** 135,000 × $0.25 / 1,000,000 = **$0.03/month**
- **Storage:** 1 GB × $0.25 = **$0.25/month**

**Total:** **$0.39/month**

**Notes:**
- On-demand pricing chosen for predictable costs
- No capacity planning required
- Scales automatically with usage

---

#### 4. AWS Amplify Hosting - $0.00/month

**Free Tier:**
- 1,000 build minutes per month
- 5 GB stored on CDN
- 15 GB data transfer out
- 500,000 requests per month

**Usage:**
- Build minutes: 20 minutes (4 builds × 5 min each)
- Storage: ~0.1 GB (React SPA build artifacts)
- Data transfer: ~10 GB
- Requests: ~50,000/month

**Pricing Beyond Free Tier:**
- Build minutes: $0.01 per minute
- Storage: $0.023 per GB
- Data transfer: $0.15 per GB
- Requests: $0.30 per million

**Status:** ✅ **Entirely within free tier**

---

#### 5. Amazon S3 - $0.02/month

**Pricing (ap-southeast-1):**
- Storage (Standard): $0.023 per GB
- PUT/COPY/POST requests: $0.005 per 1,000
- GET requests: $0.0004 per 1,000

**Usage & Cost:**
- **Storage:** 0.5 GB × $0.023 = **$0.012/month**
- **PUT Requests:** ~1,000 × $0.005 / 1,000 = **$0.005/month**
- **GET Requests:** ~5,000 × $0.0004 / 1,000 = **$0.002/month**

**Total:** **$0.02/month**

**Notes:**
- Minimal storage with 100 users
- Direct uploads via presigned URLs (efficient)

---

#### 6. CloudWatch - $0.00/month

**Free Tier:**
- 5 GB log ingestion
- 10 custom metrics
- 1,000,000 API requests

**Usage:**
- Log ingestion: ~2 GB/month (Lambda logs)
- Custom metrics: 0 (using only default metrics)

**Pricing Beyond Free Tier:**
- Log ingestion: $0.50 per GB
- Log storage: $0.03 per GB

**Status:** ✅ **Entirely within free tier**

---

### Total Monthly Cost Summary

| Service | Year 1 (Free Tier) | Year 2+ (Steady State) | % of Total |
|---------|-------------------|------------------------|------------|
| Lambda | $0.00 | $0.00 | 0% |
| API Gateway | $0.00 | $0.23 | 8% |
| DynamoDB | $0.39 | $0.39 | 13% |
| Amplify Hosting | $0.00 | $0.00 | 0% |
| S3 | $0.02 | $0.02 | 1% |
| Secrets Manager | $1.53 | $1.53 | 52% |
| CloudWatch | $0.00 | $0.00 | 0% |
| **TOTAL** | **$1.94/month** | **$2.17/month** | **100%** |

**Annual Cost:**
- **Year 1:** $23.28/year ($1.94/month)
- **Year 2+:** $26.04/year ($2.17/month)

**Cost per User (100 DAU):**
- **Year 1:** $0.0194 per user per month
- **Year 2+:** $0.0217 per user per month

---

#### Future Scaling Considerations

**At 1,000 DAU (10x growth):**
- Lambda: Still free tier (~$0.10/month)
- API Gateway: $2.30/month
- DynamoDB: $3.90/month (reads/writes scale linearly)
- S3: $0.12/month
- Secrets Manager: $0.50/month (with caching)
- **Total:** ~$7/month ($0.007 per user)

**At 10,000 DAU (100x growth):**
- Lambda: $15/month
- API Gateway: $23/month
- DynamoDB: $39/month
- S3: $1.20/month
- Amplify: $5/month (data transfer exceeds free tier)
- Secrets Manager: $0.50/month
- CloudWatch: $2/month
- **Total:** ~$86/month ($0.0086 per user)

**Cost scales sub-linearly** - per-user cost decreases as usage grows.

---

### Pricing Sources

All pricing verified from official AWS documentation (January 2026):
- Lambda: https://aws.amazon.com/lambda/pricing/
- API Gateway: https://aws.amazon.com/api-gateway/pricing/
- DynamoDB: https://aws.amazon.com/dynamodb/pricing/on-demand/
- Amplify: https://aws.amazon.com/amplify/pricing/
- S3: https://aws.amazon.com/s3/pricing/
- Secrets Manager: https://aws.amazon.com/secrets-manager/pricing/
- CloudWatch: https://aws.amazon.com/cloudwatch/pricing/

---


## Conclusion

AscendHR is built on a modern, scalable, and cost-effective serverless architecture that leverages AWS best practices. The infrastructure provides:

**Key Strengths:**
- ✅ **Exceptional Cost Efficiency** - $2/month for 100 users, $0.02 per user
- ✅ **Zero Infrastructure Management** - Fully serverless, no servers to patch
- ✅ **Auto-Scaling** - Handles 100 to 10,000+ users without changes
- ✅ **High Availability** - Multi-AZ deployments by default
- ✅ **Fast Development** - Modern frameworks, TypeScript, automated deployments
- ✅ **Secure by Default** - Encryption, IAM, least privilege access

