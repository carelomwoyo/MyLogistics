<template>
  <fragment>
    <div class="row">
      <div class="col-lg-4 col-xlg-3 col-md-5">
        <div class="card">
          <div class="card-body">
            <center class="m-t-30">
              <img
                src="https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-alt-512.png"
                class="rounded-circle"
                width="100"
              />
              <h4 class="card-title m-t-10">{{ customer.name }}</h4>
              <h6 class="card-subtitle">
                <div
                  class="badge badge-pill badge-success font-16"
                  v-if="customer.status == true"
                >
                  <span class="ti-user text-success"></span>
                  Active
                </div>

                <div
                  class="badge badge-pill badge-success font-16"
                  v-else-if="customer.status == false"
                >
                  <span class="ti-user text-success"></span>
                  Inactive
                </div>
              </h6>
            </center>
          </div>
          <div>
            <hr />
          </div>
          <div class="card-body">
            <small class="text-muted">E-mail</small>
            <h6>{{ customer.email }}</h6>
            <small class="text-muted p-t-30 db">Phone</small>
            <h6>{{ customer.phone }}</h6>
            <small class="text-muted p-t-30 db">Address</small>
            <h6>{{ customer.address }}</h6>
          </div>
          <div class="card-body row">
            <div class="col-12">
              <p class="font-s">
                Registration Date:
                {{ moment(customer.created_at).format("YYYY-MM-DD") }}
              </p>
              <p></p>
            </div>
          </div>
        </div>
      </div>

      <div class="col-lg-8 col-xlg-9 col-md-7">
        <div class="card">
          <div class="card-body">
            <div id="loader" style="display: none"></div>
            <div id="msgholder"></div>
            <div class="row mb-4">
              <Navigation></Navigation>
            </div>
            <div class="row">
              <div class="col-xl-4 col-md-6 mb-4">
                <div class="card border-left-primary shadow h-100 py-2">
                  <div class="card-body">
                    <div class="row no-gutters align-items-center">
                      <div class="col mr-2">
                        <div
                          class="text-xs font-weight-bold text-danger text-uppercase mb-1"
                        >
                          Outstanding Invoices
                        </div>
                        <div class="h5 mb-0 font-weight-bold text-gray-800">
                          ₹ {{ shipmentsInfo.outstanding_invoice }}
                        </div>
                      </div>
                      <div class="col-auto">
                        <i class="fas fa-rupee-sign fa-2x text-gray-300"></i>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-xl-4 col-md-6 mb-4">
                <div class="card border-left-success shadow h-100 py-2">
                  <div class="card-body">
                    <div class="row no-gutters align-items-center">
                      <div class="col mr-2">
                        <div
                          class="text-xs font-weight-bold text-success text-uppercase mb-1"
                        >
                          Paid Invoices
                        </div>
                        <div class="h5 mb-0 font-weight-bold text-gray-800">
                          ₹ {{ shipmentsInfo.paid_invoice }}
                        </div>
                      </div>
                      <div class="col-auto">
                        <i class="fas fa-rupee-sign fa-2x text-gray-300"></i>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-xl-4 col-md-6 mb-4">
                <div class="card border-left-info shadow h-100 py-2">
                  <div class="card-body">
                    <div class="row no-gutters align-items-center">
                      <div class="col mr-2">
                        <div
                          class="text-xs font-weight-bold text-primary text-uppercase mb-1"
                        >
                          Total Invoices
                        </div>
                        <div class="row no-gutters align-items-center">
                          <div class="col-auto">
                            <div
                              class="h5 mb-0 mr-3 font-weight-bold text-gray-800"
                            >
                              {{ shipmentsInfo.total_invoice }}
                            </div>
                          </div>
                          <div class="col">
                            <div class="progress progress-sm mr-2">
                              <div
                                role="progressbar"
                                aria-valuenow="50"
                                aria-valuemin="0"
                                aria-valuemax="100"
                                class="progress-bar bg-info"
                                style="width: 50%"
                              ></div>
                            </div>
                          </div>
                        </div>
                      </div>
                      <div class="col-auto">
                        <i
                          class="fas fa-clipboard-list fa-2x text-gray-300"
                        ></i>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="card mb-4 mt-2">
          <div class="card-header py-3">
            <h6 class="m-0 font-weight-bold text-primary">Invoices</h6>
          </div>
          <div class="card-body">
            <div class="table-responsive">
              <div
                id="dataTable_wrapper"
                class="dataTables_wrapper dt-bootstrap4"
              >
                <div class="row">
                  <div class="col-sm-12">
                    <table
                      class="table table-bordered dataTable"
                      id="dataTable"
                      width="100%"
                      cellspacing="0"
                      role="grid"
                      aria-describedby="dataTable_info"
                      style="width: 100%"
                    >
                      <thead>
                        <tr role="row">
                          <th
                            class="sorting_asc"
                            tabindex="0"
                            aria-controls="dataTable"
                            rowspan="1"
                            colspan="1"
                            aria-sort="ascending"
                            aria-label="Name: activate to sort column descending"
                            style="width: 58px"
                          >
                            Frieght Invoice No
                          </th>
                          <th
                            class="sorting"
                            tabindex="0"
                            aria-controls="dataTable"
                            rowspan="1"
                            colspan="1"
                            aria-label="Position: activate to sort column ascending"
                            style="width: 40px"
                          >
                            Date
                          </th>

                          <th
                            class="sorting"
                            tabindex="0"
                            aria-controls="dataTable"
                            rowspan="1"
                            colspan="0.2"
                            aria-label="Age: activate to sort column ascending"
                            style="width: 31px"
                          >
                            Amount
                          </th>
                          <th
                            class="sorting"
                            tabindex="0"
                            aria-controls="dataTable"
                            rowspan="1"
                            colspan="0.2"
                            aria-label="Age: activate to sort column ascending"
                            style="width: 31px"
                          >
                            Status
                          </th>
                          <th
                            class="text-center"
                            tabindex="0"
                            aria-controls="dataTable"
                            rowspan="1"
                            colspan="1"
                            aria-label="Start date: activate to sort column ascending"
                            style="width: 69px"
                          >
                            Action
                          </th>
                        </tr>
                      </thead>
                      <tfoot>
                        <tr>
                          <th rowspan="1" colspan="1">Frieght Invoice No</th>
                          <th rowspan="1" colspan="1">Date</th>

                          <th rowspan="1" colspan="1">Amount</th>
                          <th rowspan="1" colspan="1">Status</th>
                          <th rowspan="1" colspan="1" class="text-center">
                            Action
                          </th>
                        </tr>
                      </tfoot>
                      <tbody>
                        <tr
                          v-if="shipmentsInfo"
                          v-for="shipment in shipmentsInfo.shipment"
                        >
                          <td>{{ shipment.freight_invoice_number }}</td>
                          <td>{{ shipment.date }}</td>

                          <td>{{ shipment.charge_total }}</td>
                          <td>
                            <span class="badge badge-success">{{
                              shipment.status.status
                            }}</span>
                            <span
                              class="badge badge-pill badge-danger"
                              v-if="shipment.total_paid <= 0"
                              >Pending</span
                            >
                            <span
                              class="badge badge-pill badge-success"
                              v-else-if="
                                shipment.total_paid >= shipment.charge_total
                              "
                              >Paid</span
                            >

                            <span class="badge badge-pill badge-warning" v-else
                              >Partial</span
                            >
                          </td>
                          <td align="center">
                            <router-link
                              :to="'/customer/invoice/' + shipment.id + '/view'"
                              data-toggle="tooltip"
                              data-placement="top"
                              title="View Invoice"
                            >
                              <i class="fas fa-eye text-secondary"></i>
                            </router-link>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      class="modal fade"
      id="paymentmodal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Payment Details</h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row">
              <div class="input-group m-2">
                <select
                  class="custom-select"
                  id="inputGroupSelect04"
                  aria-label="Example select with button addon"
                >
                  <option selected disabled>Received From</option>
                  <option value="1">Consignor</option>
                  <option value="2">Consignee</option>
                  <option value="3">Others</option>
                </select>
              </div>
              <div class="col-md-4">
                <div class="form-group">
                  <label for="Serial Number">Payment Date</label>

                  <input type="text" class="form-control" value="31/05/2020" />
                </div>
              </div>
              <div class="col-md-4">
                <div class="form-group">
                  <label for="Size">Payment Type</label>
                  <select
                    class="custom-select"
                    id="inputGroupSelect04"
                    aria-label="Example select with button addon"
                  >
                    <option selected disabled>Choose</option>
                    <option value="1">Cash</option>
                    <option value="2">Bank</option>
                    <option value="3">UPI</option>
                    <option value="3">Cheque</option>
                  </select>
                </div>
              </div>
              <div class="col-md-4">
                <div class="form-group">
                  <label for="Size">Amount</label>
                  <input type="text" class="form-control" />
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-dismiss="modal"
            >
              Close
            </button>
            <button type="button" class="btn btn-primary">Add</button>
          </div>
        </div>
      </div>
    </div>
  </fragment>
</template>

<style scoped>
.router-link-exact-active {
  background-color: #4e73df;
  color: white;
}
</style>

<script>
import { mapGetters } from "vuex";
import Navigation from "./Navigation";
export default {
  data() {
    return {};
  },
  components: {
    Navigation,
  },
  computed: {
    ...mapGetters({
      customer: "getSingleCustomer",
      shipmentsInfo: "getCustomerInvoices",
    }),
  },
  created() {},
  mounted() {
    this.$store.dispatch(
      "retrieveCustomerInvoice",
      this.$store.getters.getUserData.user.id
    );

    this.$store.dispatch(
      "retrieveSingleCustomer",
      this.$store.getters.getUserData.user.id
    );
  },
  methods: {},
};
</script>