<template>
  <h1>
    BootcampMatch: Enroll at the perfect tech bootcamp for you in 30 minutes or
    less
  </h1>
  <table>
    <tr>
      <th>Name</th>
      <th>Total placement in 90 days for graduated job seekers</th>
      <th>Offers ISA</th>
      <th>ISA Upfront Fee</th>
    </tr>
    <tr v-for="school in schools" :key="school.id">
      <td>
        <a :href="school.url">{{ school.name }}</a>
      </td>
      <td>
        <span
          v-if="
            school.most_recent_public_total_placement_in_90_days_rate_for_graudated_job_seekers
          "
        >
          {{
            school.most_recent_public_total_placement_in_90_days_rate_for_graudated_job_seekers *
            100
          }}%</span
        >
      </td>
      <td>{{ school.does_offer_isa }}</td>
      <td>
        <span v-if="!isNaN(school.isa_up_front_fee)"
          >${{ school.isa_up_front_fee.toLocaleString() }}</span
        >
      </td>
    </tr>
  </table>
</template>

<script>
import alasql from "alasql";

var data = [
  {
    name: "Lambda School",
    url: "https://lambdaschool.com/",
    does_ISA_exclude_california: true,
    most_recent_public_total_placement_in_90_days_rate_for_graudated_job_seekers: 0.61,
    most_recent_public_total_placement_in_180_days_rate_for_graudated_job_seekers: 0.81,
    are_there_paid_team_leads: false,
    latest_public_outcomes_report_auditor_name: "The MFA Companies",
    latest_public_outcomes_report_auditor_url: "https://themfacompanies.com",
    isa_up_front_fee: 0,
    isa_payment_earliest_start_after_x_months: 0,
    were_there_any_significant_changes_after_last_public_outcomes_data_period: true,
  },
  {
    name: "Galvanize",
    url: "https://galvanize.com",
    isa_up_front_fee: 2000,
    isa_payment_earliest_start_after_x_months: 3,
  },
  { name: "Flatiron", url: "https://flatiron.com" },
  { name: "Pathrise", url: "https://pathrise.com" },
  { name: "Interview Kickstart", url: "https://interviewkickstart.com" },
  { name: "Coding Dojo", url: "https://codingdojo.com" },
  { name: "Thinkful", url: "https://thinkful.com" },
  { name: "Springboard", url: "https://springboard.com" },
  { name: "DigitalCrafts", url: "https://digitalcrafts.com" },
];

export default {
  name: "App",
  data() {
    return {
      schools: [],
    };
  },
  created: function () {
    this.schools = alasql("SELECT * FROM ? ORDER BY name", [data]);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
table {
  border-collapse: collapse;
}
th,
td {
  vertical-align: top;
  padding: 5px;
  text-align: left;
  border: 1px solid #000;
}
</style>
