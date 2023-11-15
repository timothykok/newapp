<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { getUserId } from '../../../utils/auth.js';
    let formErrors = {};

    

    async function createJob(evt) {
      evt.preventDefault()

      console.log(evt.target['minAnnualCompensation'].value)

      const userData = {
        title: evt.target['jobtitle'].value,
        minAnnualCompensation: evt.target['minAnnualCompensation'].value,
        maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
        description: evt.target['description'].value,
        requirements: evt.target['requirements'].value,
        employer: evt.target['employer'].value,
        location: evt.target['location'].value,
        applicationInstructions: evt.target['applicationInstructions'].value,
        user: getUserId()
      };
      
      const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(userData)
      });

      console.log(resp)
      let res = await resp.json();
  
      if (resp.status == 200) {
          let jobId = res.id
          console.log(jobId)
          goto(`/jobs/${jobId}`);
        } 
    }
  </script>
  

  <div class= "p-14" >
    <h1 class="text-left text-3xl">Post A Job</h1>
    <div class="text-left">
        <p> Find Your Next Hire Here</p>
    </div>
    <div class="flex justify-left items-center mt-8 h-full pr-64 pb-7">
        <form on:submit={createJob} class="w-full">
            <div class="form-control w-full">
              <label class="label" for="title">
                  <span class="label-text">Job Title</span>
              </label>
              <input type="text" name="jobtitle" placeholder="Software Engineer" class="input input-bordered w-full" required />
              {#if 'title' in formErrors}
              <label class="label" for="title">
                  <span class="label-text-alt text-red-500">{formErrors['jobtitle'].message}</span>
              </label>
              {/if}
          </div>

          <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Min Compensation Range</span>
            </label>
            <input type="number" name="minAnnualCompensation" placeholder="3000" class="input input-bordered w-full" required />
            {#if 'minAnnualCompensation' in formErrors}
            <label class="label" for="title">
                <span class="label-text-alt text-red-500">{formErrors['minAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>



    
        <div class="form-control w-full">
          <label class="label" for="title">
              <span class="label-text">Max Compensation Range</span>
          </label>
          <input type="number" name="maxAnnualCompensation" placeholder="10,000" class="input input-bordered w-full" required />
          {#if 'maxAnnualCompensation' in formErrors}
          <label class="label" for="title">
              <span class="label-text-alt text-red-500">{formErrors['maxAnnualCompensation'].message}</span>
          </label>
          {/if}
      </div>

  

            <div class="form-control w-full">
              <label class="label" for="employer">
                  <span class="label-text">Company Name</span>
              </label>
              <input type="text" name="employer" placeholder="e.g. Facebook" class="input input-bordered w-full" required />
              {#if 'employer' in formErrors}
              <label class="text" for="employer">
                  <span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="label" for="location">
                  <span class="label-text">Job Location</span>
              </label>
              <input type="text" name="location" placeholder="e.g. Singapore" class="input input-bordered w-full" required />
              {#if 'location' in formErrors}
              <label class="text" for="location">
                  <span class="label-text-alt text-red-500">{formErrors['email'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="text" for="description">
                  <span class="label-text">Description</span>
              </label>
              <input type="text" name="description" class="input input-bordered w-full h-60 align-text-top" required />
              {#if 'description' in formErrors}
              <label class="text" for="description">
                  <span class="label-text-alt text-red-500">{formErrors['Description'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="text" for="requirements">
                  <span class="label-text">Requirements</span>
              </label>
              <input type="text" name="requirements"  class="input input-bordered w-full h-40 align-text-top" required />
              {#if 'requirements' in formErrors}
              <label class="text" for="requirements">
                  <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="text" for="applicationInstructions">
                  <span class="label-text">Application Instructions</span>
              </label>
              <input type="text" name="applicationInstructions" class="input input-bordered w-full h-20 align-text-top" required />
              {#if 'applicationInstructions' in formErrors}
              <label class="text" for=" applicationInstructions">
                  <span class="label-text-alt text-red-500">{formErrors['applicationInstructions'].message}</span>
              </label>
              {/if}
            </div>
    
            <div class="form-control w-64 mt-4 float-right">
              <button class="btn btn-neutral" >Post Job</button>

              
              
            
            </div>
        </form>
    </div>
</div>