---
date: 2025-03-17T14:00:00Z
title: "Job Listings With Filtering: A Frontend Mentor Challenge"
description: "Learn how to create a job listings app using React. Features include job filtering."
image: "../../assets/images/25/03/job-listings-app.jpg"
categories: ["React"]
authors: ["Brandford"]
tags: ["nextjs","react","javascript","typescript"]
series: ["React Tutorials", "1"]
canonical: "https://www.codetidehub.com/job-listings-with-filtering/"
---

In this guide, we will learn how to create a job listings app using React and tailwind css. Let's dive into this short tutorial.

---

## Create A Nextjs App

To install a Nextjs app, run the command below in your terminal.

```bash
npm create-next-app@latest job-listings-app
```

Follow the subsequent instructions after running the command to complete the process.
We will be using the **src** folder so make sure you select yes when asked during the process.

## Setting Up Our Files, Folders, And Components

### Delete Automatically Generated Code By Nextjs

#### Modify code in page.tsx file

Open the page.tsx file, remove all the generated code and paste the code below;
Visit [localhost](localhost:3000) and you will see Hello world printed on your screen.

```tsx
//page.tsx

export default function Home() {
  return <main className="flex justify-center h-screen">Hello</main>;
}
```

#### Modify code in layout.tsx file

In the layout.tsx, let's also delete the previous code and paste the code below;

```tsx
//layout.tsx

import type { Metadata } from "next";
import { Geist, Geist_Mono } from "next/font/google";
import "./globals.css";

const geistSans = Geist({
  variable: "--font-geist-sans",
  subsets: ["latin"],
});

const geistMono = Geist_Mono({
  variable: "--font-geist-mono",
  subsets: ["latin"],
});

export const metadata: Metadata = {
  title: "Job Listings App",
  description: "Find new software engineering job listings",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body
        className={`${geistSans.variable} ${geistMono.variable} antialiased `}
      >
        {children}
      </body>
    </html>
  );
}
```

You can customise colors, fonts, and page titles, to suit your needs.

#### 1. Create A data.json file

Inside the **app** folder, create a **component** folder, This folder who contain the job listings json provided by **Frontend Mentor**.
This is how the json looks like;

```json
[
  {
    "id": 1,
    "company": "Photosnap",
    "logo": "./images/photosnap.svg",
    "new": true,
    "featured": true,
    "position": "Senior Frontend Developer",
    "role": "Frontend",
    "level": "Senior",
    "postedAt": "1d ago",
    "contract": "Full Time",
    "location": "USA Only",
    "languages": ["HTML", "CSS", "JavaScript"],
    "tools": []
  },
  {
    "id": 2,
    "company": "Manage",
    "logo": "./images/manage.svg",
    "new": true,
    "featured": true,
    "position": "Fullstack Developer",
    "role": "Fullstack",
    "level": "Midweight",
    "postedAt": "1d ago",
    "contract": "Part Time",
    "location": "Remote",
    "languages": ["Python"],
    "tools": ["React"]
  },
  {
    "id": 3,
    "company": "Account",
    "logo": "./images/account.svg",
    "new": true,
    "featured": false,
    "position": "Junior Frontend Developer",
    "role": "Frontend",
    "level": "Junior",
    "postedAt": "2d ago",
    "contract": "Part Time",
    "location": "USA Only",
    "languages": ["JavaScript"],
    "tools": ["React", "Sass"]
  }
]
```

#### Create components folder

Let's create a folder in the src folder and name it **components**. Inside this folder, we will be creating 3 new components;

1. header.tsx
2. job-card.tsx
3. filter.tsx

Let's start with our header.tsx component. The code for this component will look like this.

```tsx
//header.tsx

import React from "react";

const Header = () => {
  return;
  <div>Header</div>;
};

export default Header;
```

Next is our `job-card.tsx`. The code for this component is below;

```tsx

//job-card.tsx

import Image from "next/image";
import React from "react";

const JobCard = () => {
  return (
    <div>Job Card</>
  );
};

export default JobCard;

```

The final component is the `filter.tsx` . The code is below;

```tsx
//filter.tsx

cconst Filter = () => {
  return (
    <div>Filter</>
  );
};



export default Filter;

```

## Implementing The Job Filtering Functionalities

### Working on the job-card component

Our `job-card.tsx` component will look like this after our final code implementation.

```tsx
//job-card.tsx final code

import Image from "next/image";
import React from "react";

const JobCard = ({
  img,
  company,
  contract,
  position,
  featured,
  level,
  role,
  languages,
  tools,
  location,
  New,
  postedAt,
  addFilter,
}: {
  img: string;
  company: string;
  contract: string;
  position: string;
  featured: boolean;
  level: string;
  languages: string[];
  tools: string[];
  location: string;
  role: string;
  New: boolean;
  postedAt: string;
  addFilter: (filter: string) => void;
}) => {
  return (
    <div className="border border-l-2 border-l-green-700 border-white text-sm rounded-md bg-white h-[100px] w-full p-5 flex justify-between mb-10 shadow-md">
      <section className="left flex ">
        <Image
          width={50}
          height={50}
          src={img.split("/").pop() as string}
          priority
          alt="company"
          className="rounded-full"
        />
        <section className="flex flex-col space-y-1">
          <section className="flex space-x-2">
            <p className="font-bold text-cyan-400">{company}</p>
            <div className="capitalize">
              {New === true ? <p>New</p> : <p>Old</p>}
            </div>
            <p className="capitalize">{featured === true ? "true" : "false"}</p>
          </section>
          <section className="text-center flex font-bold">
            <p>{position}</p>
          </section>
          <section className="flex space-x-2">
            <p>{postedAt}</p>
            <p>{contract}</p>
            <p>{location}</p>
          </section>
        </section>
      </section>
      <section className="right flex space-x-2 justify-center items-center text-sm text-cyan-400 ">
        {[role, level, ...languages, ...tools].map((filter) => (
          <button
            type="button"
            key={filter}
            onClick={() => addFilter(filter)}
            className="bg-cyan-100 p-2 rounded-md hover:bg-cyan-200 cursor-pointer"
          >
            {filter}
          </button>
        ))}
      </section>
    </div>
  );
};

export default JobCard;
```

Next, let's work on the `filter.tsx` component.

### Working on the filter component

The filter component code is below;

```tsx
//filter.tsx

const Filter = ({
  filters,
  removeFilter,
  clearFilters,
}: {
  filters: string[];
  removeFilter: (filter: string) => void;
  clearFilters: () => void;
}) => {
  return (
    <div className="bg-white p-4 rounded-md shadow-md flex items-center space-x-2 w-full max-w-4xl my-5">
      {filters.map((filter) => (
        <div
          key={filter}
          className="flex items-center bg-cyan-100 p-2 rounded-md"
        >
          <span className="text-cyan-700">{filter}</span>
          <button
            type="submit"
            onClick={() => removeFilter(filter)}
            className="ml-2 text-red-500 cursor-pointer"
          >
            ✕
          </button>
        </div>
      ))}
      <button
        type="submit"
        onClick={clearFilters}
        className="ml-auto text-blue-500 font-semibold cursor-pointer"
      >
        Clear
      </button>
    </div>
  );
};

export default Filter;
```

Next, we will also need to work on the `page.tsx` which is the homepage of the web app.

### Working On The page.tsx file

In `page.tsx`, we will add three functions, **addFilter**, **removeFilter**, and **clearFilter**. We will use react **useState** to handle adding, removing, and clearing filters. The code is below;

```tsx
const [filters, setFilters] = useState<string[]>([]);

const filteredJobs = jobs.filter((job) =>
  filters.every(
    (filter) =>
      job.company.toLowerCase().includes(filter.toLowerCase()) ||
      job.role.toLowerCase().includes(filter.toLowerCase()) ||
      job.level.toLowerCase().includes(filter.toLowerCase()) ||
      job.languages.includes(filter) ||
      job.tools.includes(filter)
  )
);

const addFilter = (filter: string) => {
  if (!filter.includes(filter.toLowerCase())) {
    setFilters([...filters, filter]);
  }
};

const removeFilter = (filter: string) => {
  setFilters(filters.filter((f) => f !== filter));
};

const clearFilters = () => {
  setFilters([]);
};
```

The final code of the `page.tsx` is below;

```tsx
"use client";
import Header from "@/components/header";
import JobCard from "@/components/job-card";
import jobs from "./data.json";
import Search from "@/components/search";
import { useState } from "react";

export default function Home() {
  const [filters, setFilters] = useState<string[]>([]);

  const filteredJobs = jobs.filter((job) =>
    filters.every(
      (filter) =>
        job.company.toLowerCase().includes(filter.toLowerCase()) ||
        job.role.toLowerCase().includes(filter.toLowerCase()) ||
        job.level.toLowerCase().includes(filter.toLowerCase()) ||
        job.languages.includes(filter) ||
        job.tools.includes(filter)
    )
  );

  const addFilter = (filter: string) => {
    if (!filter.includes(filter.toLowerCase())) {
      setFilters([...filters, filter]);
    }
  };

  const removeFilter = (filter: string) => {
    setFilters(filters.filter((f) => f !== filter));
  };

  const clearFilters = () => {
    setFilters([]);
  };

  console.log(filteredJobs);

  return (
    <main className="flex justify-center h-screen">
      <section>
        <Header />
        {filters.length > 0 && (
          <Search
            filters={filters}
            removeFilter={removeFilter}
            clearFilters={clearFilters}
          />
        )}

        {filteredJobs.map((job) => {
          return (
            <div key={job.company}>
              <JobCard
                img={job.logo}
                company={job.company}
                contract={job.contract}
                featured={job.featured}
                level={job.level}
                position={job.position}
                languages={job.languages}
                role={job.role}
                location={job.location}
                New={job.new}
                postedAt={job.postedAt}
                tools={job.tools}
                addFilter={addFilter}
              />
            </div>
          );
        })}
      </section>
    </main>
  );
}
```

That's all for this tutorial, let's run the app and open [localhost](https:localhost:3000) and your app will work fine.
