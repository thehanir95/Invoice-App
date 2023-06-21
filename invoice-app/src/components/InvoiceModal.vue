<template>
  <div @click="checkClick" ref="invoiceWrap" class="invoice-wrap">
    <form @submit.prevent="submitForm" class="invoice-content">
      <h1>New Invoice</h1>
      <div class="bill-from">
        <h4>Bill From</h4>
        <div class="input">
          <label for="billerStreetAddress">Street Address</label>
          <input
            required
            type="text"
            id="billerStreetAddress"
            v-model="billerStreetAddress"
          />
        </div>
        <div class="location-details">
          <div class="input">
            <label for="billerCity">City</label>
            <input required type="text" id="billerCity" v-model="billerCity" />
          </div>
          <div class="input">
            <label for="billerZipCode">Zip code</label>
            <input
              required
              type="text"
              id="billerZipCode"
              v-model="billerZipCode"
            />
          </div>
          <div class="input">
            <label for="billerCountry">Country</label>
            <input
              required
              type="text"
              id="billerCountry"
              v-model="billerCountry"
            />
          </div>
        </div>
      </div>

      <div class="bill-to">
        <h4>Bill To</h4>
        <div class="input">
          <label for="clientName">Client Name</label>
          <input required type="text" id="clientName" v-model="clientName" />
        </div>
        <div class="input">
          <label for="clientEmail">Client Email</label>
          <input required type="email" id="clientEmail" v-model="clientEmail" />
        </div>
        <div class="input">
          <label for="clientStreetAddress">Client Street Address</label>
          <input
            required
            type="text"
            id="clientStreetAddress"
            v-model="clientStreetAddress"
          />
        </div>
        <div class="location-details">
          <div class="input">
            <label for="clientCity">Client City</label>
            <input required type="text" id="clientCity" v-model="clientCity" />
          </div>
          <div class="input">
            <label for="clientZipCode">Client ZipCode</label>
            <input
              required
              type="text"
              id="clientZipCode"
              v-model="clientZipCode"
            />
          </div>
          <div class="input">
            <label for="clientCountry">Client Country</label>
            <input
              required
              type="text"
              id="clientCountry"
              v-model="clientCountry"
            />
          </div>
        </div>
      </div>

      <div class="invoice-work">
        <div class="payment">
          <div class="input">
            <label for="invoiceDate">Invoice Date</label>
            <input
              disabled
              type="text"
              id="invoiceDate"
              v-model="invoiceDate"
            />
          </div>
          <div class="input">
            <label for="paymentDueDate">Payment DueDate</label>
            <input
              disabled
              type="text"
              id="paymentDueDate"
              v-model="paymentDueDate"
            />
          </div>
        </div>
        <div class="input">
          <label for="paymentTerms">Payment Terms</label>
          <select required type="text" id="paymentTerms" v-model="paymentTerms">
            <option value="30">Net 30 Days</option>
            <option value="30">Net 60 Days</option>
          </select>
        </div>
        <div class="input">
          <label for="productDescription">Product Description</label>
          <input
            required
            type="text"
            id="productDescription"
            v-model="productDescription"
          />
        </div>
        <div class="work-items">
          <h3>Item List</h3>
          <table class="item-list">
            <tr class="table-heading">
              <th class="item-name">Item Name</th>
              <th class="item-name">Qty</th>
              <th class="item-name">Price</th>
              <th class="item-name">Total</th>
            </tr>
            <tr
              class="table-items"
              v-for="(item, index) in invoceItemsList"
              :key="index"
            >
              <td class="item-name">
                <input type="text" v-model="item.itemName" />
              </td>
              <td class="qty">
                <input type="text" v-model="item.Qty" />
              </td>
              <td class="price">
                <input type="text" v-model="item.price" />
              </td>
              <td class="total">
                ${{ (item.total = item.Qty * item.price) }}
              </td>
              <img @click="deleteInvoiceItem(item.id)" src="../assets/icon-delete.svg" alt="delete-icon">
            </tr>
          </table>
          <div class="btn-section" @click="addNewInvoiceItem">
            <img src="../assets/icon-plus.svg" alt="plus-icon">Add New Item
          </div>
        </div>
      </div>
      <div class="save-exit-section">
        <div class="close-btn-section">
            <button type="button" class="btn btn-danger" @click="closeInvoice">Cancel</button>
        </div>
        <div class="save-btn-section">
            <button type="button" class="btn btn-success" @click="saveDraftInvoice">Save Draft</button>
            <button type="button" class="btn btn-primary" @click="publishInvoice">Create Invoice</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { mapMutations } from 'vuex';
export default {
  name: "InvoiceModal",
  data() {
    return {
      billerStreetAddress: null,
      billerCity: null,
      billerZipCode: null,
      billerCountry: null,
      clientName: null,
      clientEmail: null,
      clientStreetAddress: null,
      clientCity: null,
      clientZipCode: null,
      clientCountry: null,
      invoiceDateUnix: null,
      invoiceDate: null,
      paymentTerms: null,
      paymentDueDateUnix: null,
      paymentDueDate: null,
      productDescription: null,
      invoicePending: null,
      invoiceDraft: null,
      invoiceItemList: [],
      invoiceTotal: 0,
    };
  },
  methods:{
    ...mapMutations(['TOGGLE_INVOICE']),
    closeInvoice(){
        this.TOGGLE_INVOICE();
    }
  }
};
</script>

<style lang="scss" scoped>
.invoice-wrap {
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 0;
  left: 0;
  background-color: transparent;
  width: 100%;
  height: 100vh;
  overflow: scroll;
  text-align: left;
  @media (min-width: 900px){
    left: 90px;
    overflow: hidden;
  }
  .invoice-content{
    position: relative;
    padding: 56px;
    max-width: 700px;
    width: 100%;
    background-color: #414165;
    color: #fff;
    box-shadow: 10px 4px 6px -1px rgba(0,0,0,0.2),0 2px 4px  -1px rgba(0,0,0,0.06);
    overflow-y: scroll;
  }

  h1{
    margin-bottom: 48px;
    color: #fff;
  }

  h3{
    margin-bottom: 16px;
    color: #777f98;
    font-size: 18px;
  }

  h4{
    color: #7c5dfa;
    font-size: 12px;
    margin-bottom: 24px;
  }

  .input {
  display: flex;
  flex-direction: column;
  margin-bottom: 24px;
}
label{
    font-size: 12px;
    margin-bottom: 6px;
}

.bill-from,
.bill-to {
  display: flex;
  flex-direction: column;
  margin-bottom: 48px;

  .location-details{
    gap: 16px;
    div{
        flex: 1;
    }
  }
}

.invoice-work {
  display: flex;
  flex-direction: column;
  .payment{
    display: flex;
    gap: 24px;
    div{
        flex: 1;
    }
  }
.btn-section{
  display: flex;
}
.work-items{
    .item-list{
        width: 100%;
        .table-heading{
            margin-bottom: 16px;
        }
        .table-items{
            gap: 16px;
            font-size: 12px;
            .item-name{
                flex-basis: 50%;
            }

            .qty{
                flex-basis: 10%;
            }

            .price{
                flex-basis: 20%;
            }
            .total{
                flex-basis: 20%;
                text-align: center;
            }
        }
        .table-items {
            display: flex;
            margin-bottom: 24px;
            position: relative;

            img{
                position: absolute;
                top: 15px;
                right: 0;
                width: 12px;
                height: 16px;
            }
        }
    }

    .btn-section{
        color: #fff;
        background-color: #252945;
        align-items: center;
        justify-content: center;
        width: 100%;
        border-radius: 10px;
        padding: 5px;
        margin: 16px 0;
        img{
            margin-right: 4px;
        }
    }
}
}

input,
select{
    width: 100%;
    background: #1e2139;
    color: #fff;
    border-radius: 4px;
    padding: 12px 4px;
    border: none;

    &:focus{
        outline: none;
    }
}
}

.location-details {
  display: flex;
}

.save-exit-section{
    display: flex;
    justify-content: space-between;

    .close-btn-section{
        width: 50%;
    }
    .save-btn-section{
        display: contents;
    }
}
</style>
